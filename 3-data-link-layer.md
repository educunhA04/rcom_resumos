# DATA LINK LAYER

## Goal
- Provide communication between adjacent machines
## Main functions
- Eliminate/reduce transmission errors
- Regulate data flow
- Slow receivers not swamped by fast senders
    - Provide service to the network layer
## Services provided
- Unacknowledged connectionless service
- Acknowledged connectionless service
- Acknowledged connection-oriented service

![alt text](image.png)

![alt text](image-1.png)

# Framing
## Character (byte) count

1. **Sender**:
   - Adds a **count field** at the start of each frame.
   - The count specifies the total number of bytes in the frame, including the count field itself.
2. **Receiver**:
   - Reads the count field to determine how many bytes to expect in the frame.
   - Extracts and processes the frame accordingly.

`If the count field says `**`10`**`, but the actual frame is `**`5`**` bytes, the receiver will read extra bytes, corrupting subsequent frames.`

![alt text](image-2.png)

- O Frame 2 na imagem b deveria começar em `5`, não em `7`

## Flag bytes, with `byte stuffing`
![alt text](image-3.png)

![alt text](image-4.png)

1. **Flag Byte**:
   - A special **flag byte** is used to mark the start and end of a frame.
   - Example: The flag byte could be a unique value like `01111110` (in hexadecimal: `0x7E`).

2. **Byte Stuffing**:
   - If the flag byte or another special control byte (e.g., escape byte) appears in the actual data, it is **stuffed** with an escape byte to prevent it from being misinterpreted as a frame boundary.

## Start and end flags, with `bit stuffing`
![alt text](image-3.png)
- Semelhante ao anterior

- **Example**:
    ```
    Flag = 01111110
    
    Se no payload forem encontradas sequências com 11111, é adicionado um 0 à frente, fazendo o stuffing.

    Assim, quando os dados forem lidos, o padrão 01111110 só vai aparecer nas flags e não no payload, pelo que o fim e início do frame é detetado corretamente.

    Posteriormente, para fazer o destuffing, sempre que for encontrada uma sequência de 111110, o 0 é removido, ou seja, o payload regressa ao formato original.
    ```

# Byte Stuffing Process

## Sender:
1. Adds a **flag byte** at the beginning and end of each frame.
2. Scans the payload data for occurrences of:
   - **Flag byte** (`0x7E`).
   - **Escape byte** (`0x7D`).
3. Inserts an escape byte (`0x7D`) before any flagged bytes in the data and modifies the flagged byte:
   - `0x7E` → `0x7D 0x5E` (flag byte).
   - `0x7D` → `0x7D 0x5D` (escape byte).

## Receiver:
1. Identifies the start and end of the frame using the flag bytes.
2. Scans the payload for escape sequences:
   - `0x7D 0x5E` → `0x7E`.
   - `0x7D 0x5D` → `0x7D`.
3. Reconstructs the original data by removing escape bytes and interpreting the flagged bytes correctly.


