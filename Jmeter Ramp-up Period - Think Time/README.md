# Jmeter: Ramp-up Period & Think Time

### Ramp-up Period
* number of threads = N
* Ramp-up Period = X (seconds)
* Create X/N threads per second. After N threads created, they send request independently.

### Think Time
* Contrapose single thread.
* If Think Time = N, send request every N second(s). For example, first request will be sent at 1 second, second request will be sent at (N+1) second.

### What will happen when config both Ramp-up Period and Think Time?
* number of threads = N
* Ramp-up Period = X (seconds)
* Think Time = Y (seconds)

#### Ramp-up Period < Think Time (X < Y)
* So, Jmeter send request per N/X seconds. In X seconds, Jmeter send N requests, at Y, Jmeter send N requests again... 

#### Ramp-up Period = Think Time (X = Y)
* So, Jmeter send request at a fixed frequency. The interval between arbitrary requests is the same.

#### Ramp-up Period > Think Time (X > Y)

###### If X = m*Y m=2, 3, 4, ...
* In Y second, _Y*(X/N)_ requests have been sent, next Y to X, the rest _(m-1)Y*(X/N)_ threads created.

| 1/m (Y) | 2/m (2Y) | 3/m (3Y) | ... | m (mY) | (m+1)/m ((m+1)Y) | (m+2)/m ((m+2)Y)) | ... | ... |
| ------- |:--------:|:--------:|:---:|:------:|:----------------:|:-----------------:|:---:|----:|
| z       | z        | z        | ... | z      |                  |                   |     |     |
|         | z        | z        | ... | z      | z                |                   |     |     |
|         |          | z        | ... | z      | z                | z                 |     |     |
|         |          |          | ... | .      | .                | .                 |     |     |
|         |          |          | ... | z      | z                | z                 | ... | ... |
|         |          |          |     |        |                  |                   |     |     |
| z       | 2z       | 3z       | ... | mz     | mz               | mz                |  mz | mz  |

###### If X != m*Y m=2, 3, 4, ...
| 1 | 2 | 3 | ... | Y  | ... | X  | ... | 2Y | ... |     | ... |     | ... |
| - |:-:|:-:|:---:|:--:|:---:|:--:|:---:|:--:|:---:|:---:|:---:|:---:|----:|
| z | z | z | z   | z  | z   | z  |     |    |     |     |     |     |     |
|   |   |   |     |    | z   | z  | z   | z  | ... |     |     |     |     |
|   |   |   |     |    |     |    |     |    | z   | ... | ... | ... | ... |
|   |   |   |     |    |     |    |     |    |     |     |     |     |     |
| z | z | z |  z  | z  | 2z  | 2z | z   | z  | 2z  | 2z  |     |     |     |
