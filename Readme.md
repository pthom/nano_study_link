# Study link issue with nanobind

## Benchmark
| Platform   | Library   |   Lib Size (MB) | Options                               | Time       |
|:-----------|:----------|----------------:|:--------------------------------------|:-----------|
| linux      | pybind11  |             4.9 | default                               | 3m 21s     |
| linux      | nanobind  |             2.6 | default                               | 1m 37s     |
| windows    | pybind11  |             3.2 | default                               | 3m 02s     |
| windows    | nanobind  |             5.3 | no optim                              | 1m 59s     |
| windows    | nanobind  |             2.2 | default optim (/Os cf nanobind cmake) | 2h 28m (!) |
| windows    | nanobind  |             2.2 | /O1 (close to /Os)                    | 2h 18m (!)    |
| windows    | nanobind  |             2.2 | /Os (optim size)                      | 2h 22m (!)    |


## Benchmark in imgui-bundle

Wheels built for:
- python 3.11, 3.12 and 3.13
- macOS: arm and intel
- ubuntu: all x64 platforms (no arm, no 32 bits)
- windows: x64 (no 32 bits, nor arm). Built with /Od (no optimization)


| Library   | OS             |   Build time (min) |   Size (MB) |
|:----------|:---------------|-------------------:|------------:|
| pybind11  | macos-latest   |               50.7 |        63.3 |
| pybind11  | ubuntu-latest  |               90   |       179   |
| pybind11  | windows-latest |               29.4 |       118   |
| nanobind  | macos-latest   |               13.1 |        58.3 |
| nanobind  | ubuntu-latest  |               61   |       165   |
| nanobind  | windows-latest |               22.2 |       124   |

Total sizes for each library:

| Library   | Binary wheels Size (MB) | Source distribution (MB) |
|:----------|-------------------------|-------------------------:|
| nanobind  | 347.3                   |                     39.6 |
| pybind11  | 360.3                   |                     39.5 |

