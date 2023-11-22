# embulk-memory-leak-debug

This repository is dedicated to reproducing the memory leak issue associated with the buffer in Embulk.

ref: https://github.com/orgs/embulk/discussions/21

## steps

Duplicate multiple files from seed.csv into data/

```shell
for i in {1..10000}; do cp seed.csv data/input$i.csv; done
```

Run embulk

```shell
embulk -J-Xms512m -J-Xmx512m run config.yml
```
