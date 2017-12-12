# GenericCommunicationProtocol
## Intro
This is a generic communication protocol intended to make medical sensor development faster. The protocol is divided into a few simple fields that allow for the contextualization of medical data packets. Look at MedHub's implementation of this protocol as a beginning point for creating your own data types and using the protocol

## Byte Field Description
| Field        | Purpose           | Size (Bytes)  |
| ------------- |:-------------| ----:|
| Start of Frame     | Indicates the start of a package. Value must be 0xF0  | 1 |
| Size      | Indicates the total size of the Reserved, Type, and Data fields. Therefore, its value should be Data + 4. Note, this does **not** include the final CRC bytes.      |   1 |
| Reserved      | These bytes are currently not used and are reserved for future use. Set to 0 to ensure any future use does not conflict with legacy values set here.      |   2 |
| Type      | This signifies the type of the packet being sent. Refer to the table below for possible packet types already taken.      |   1 |
| Data | The is the actual data being transmitted through this protocol. It's context and meaning byte-by-byte depend on the type of messaged specified above.      |    Size - 4 (Maximum of 252) |
| CRC      | This is a CRC-16 calculated **from the reserved bytes to the end of the data**. It should use a final XOR value of 0x0000 and an initial value of 0x1D0F. This should be placed with the LSB being the first byte and the MSB being the second byte (Little Endian)     |   2 |

## Used Types

| Sensor        | Type           
| ------------- |:-------------:|
| Blood Pressure      | 1 |
| ECG      | 2      |
| Heart Rate | 3      |
| Breathing Rate | 4      |
| Temperature | 5      |
| Alert | 6      |
