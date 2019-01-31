# dataset-basis 
big endian dataset

## File format

### basis file (basis-v\_onemax-INDSIZE20-idx3-ubyte):  

| [offset] | [type]         | [value]    | [description]     |
|:---------|:-------------- |:---------- |:--------------    |
| 0000     | 32 bit integer | 0x00000803 | magic number      |
| 0004     | 32 bit integer | ![16\times 20\times 20][16x20x20] | the number of base    |
| 0008     | 32 bit integer | 20         | the  number of rows |
| 0012     | 32 bit integer | 20         | the  number of cols |
| 0013     | unsigned byte  | ??         | element of matrix   |
| 0014     | unsigned byte  | ??         | element of matrix   |
| ......   |                |            |                     |
| xxxx     | unsigned byte  | ??         | element of matrix   |

### epistasis file (epistasis-v\_onemax-INDSIZE20-idx1-double):  

| [offset] | [type]         | [value]    | [description]     |
|:---------|:-------------- |:---------- |:--------------    |
| 0000     | 32 bit integer | 0x00000E01 | magic number      |
| 0004     | 32 bit integer | ![16\times 20\times 20][16x20x20] | the number of items   |
| 0008     | double         | ??         | item              |
| 0016     | double         | ??         | item              |
| ......   |                |            |                   |
| xxxx     | double         | ??         | item              |

The epistasis values are 0.0 to inf.

## How to read dataset with Python

``` bash
git clone https://github.com/jazz4rabbit/dataset-basis.git
cd dataset-basis
tar -zxvf data.tar.gz
```

### basis file
``` python
import numpy as np
with open('./data/v_onemax/basis-v_onemax-INDSIZE20-idx3-ubyte' ,'br') as f:
    magic_number_basis = int.from_bytes(f.read(4), 'big')
    num_of_base = int.from_bytes(f.read(4), 'big')
    row = int.from_bytes(f.read(4), 'big')
    col = int.from_bytes(f.read(4), 'big')
    mats = np.frombuffer(f.read(), '>i2').reshape((num_of_base, row, col))
```

### epistasis file
``` python
import numpy as np
with open('./data/v_onemax/epistasis-v_onemax-INDSIZE20-idx1-double' ,'br') as f:
    magmagic_number_epistasis = int.from_bytes(f.read(4), 'big')
    num_of_epistases = int.from_bytes(f.read(4), 'big')
    fits = np.frombuffer(f.read(), '>d')
```

[16x20x20]: https://latex.codecogs.com/svg.latex?16\times&space;20\times&space;20

