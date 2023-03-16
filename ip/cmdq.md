# CMDQ

## Descriptors

### All commands

| 63  | 62  | 61  | 60  | 59     | 58     | 57     | 56     |   |
|-----|-----|-----|-----|--------|--------|--------|--------|---|
| cmd | cmd | cmd | cmd | sw int | sw int | sw int | sw int |   |
| 55  | 54  | 53  | 52  | 51     | 50     | 49     | 48     |   |
|     |     |     |     |        |        |        |        |   |
| 47  | 46  | 45  | 44  | 43     | 42     | 41     | 40     |   |
|     |     |     |     |        |        |        |        |   |
| 39  | 38  | 37  | 36  | 35     | 34     | 33     | 32     |   |
|     |     |     |     |        |        |        |        |   |
| 31  | 30  | 29  | 28  | 27     | 26     | 25     | 24     |   |
|     |     |     |     |        |        |        |        |   |
| 23  | 22  | 21  | 20  | 19     | 18     | 17     | 16     |   |
|     |     |     |     |        |        |        |        |   |
| 15  | 14  | 13  | 12  | 11     | 10     | 9      | 8      |   |
|     |     |     |     |        |        |        |        |   |
| 7   | 6   | 5   | 4   | 3      | 2      | 1      | 0      |   |
|     |     |     |     |        |        |        |        |   |

* cmd
  - 0x0 : nop
  - 0x1 : write
  - 0x2 : wait bus trigger
  - 0x3 : poll eq
  - 0xb : poll neq

* sw int - interrupt number to trigger?

## Polling commands

| 63         | 62         | 61         | 60         | 59         | 58         | 57         | 56         |   |
|------------|------------|------------|------------|------------|------------|------------|------------|---|
| cmd        | cmd        | cmd        | cmd        | sw int     | sw int     | sw int     | sw int     |   |
| 55         | 54         | 53         | 52         | 51         | 50         | 49         | 48         |   |
| riu addr h | riu addr h | riu addr h | riu addr h | riu addr h | riu addr h | riu addr h | riu addr h |   |
| 47         | 46         | 45         | 44         | 43         | 42         | 41         | 40         |   |
| riu addr m | riu addr m | riu addr m | riu addr m | riu addr m | riu addr m | riu addr m | riu addr m |   |
| 39         | 38         | 37         | 36         | 35         | 34         | 33         | 32         |   |
| riu addr l | riu addr l | riu addr l | riu addr l | riu addr l | riu addr l | riu addr l | riu addr l |   |
| 31         | 30         | 29         | 28         | 27         | 26         | 25         | 24         |   |
| value h    | value h    | value h    | value h    | value h    | value h    | value h    | value h    |   |
| 23         | 22         | 21         | 20         | 19         | 18         | 17         | 16         |   |
| value l    | value l    | value l    | value l    | value l    | value l    | value l    | value l    |   |
| 15         | 14         | 13         | 12         | 11         | 10         | 9          | 8          |   |
| mask h     | mask h     | mask h     | mask h     | mask h     | mask h     | mask h     | mask h     |   |
| 7          | 6          | 5          | 4          | 3          | 2          | 1          | 0          |   |
| mask l     | mask l     | mask l     | mask l     | mask l     | mask l     | mask l     | mask l     |   |
