# Study link issue with nanobind

## Benchmark

### macOS

With pybind11:
```
export STUDY_PYBIND11=ON
time pip install -v .
=> pip install -v .  157.87s user 8.47s system 106% cpu 2:35.60 total
```

With nanobind:
```
export STUDY_PYBIND11=OFF
time pip install -v .
=> pip install -v .  29.34s user 1.91s system 218% cpu 14.287 total
```

