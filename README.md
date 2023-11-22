# embulk-memory-leak-debug

This repository is dedicated to reproducing the memory leak issue associated with the buffer in Embulk.

ref: https://github.com/orgs/embulk/discussions/21

## steps

Duplicate multiple files from `seed.csv` into `data/`

This duplication process may take some time. In my case, with a heap allocation of 1GB, garbage collection activity increased when the number of files reached around 20,000. Depending on your needs, you may adjust the heap allocation size and the number of target files.

```shell
for i in {1..30000}; do cp seed.csv data/input$i.csv; done
```

Run embulk with explicit heap memory allocation.

Additionally, because the results may vary depending on the number of CPU cores in each environment, the `exec.max_threads` and `exec.min_output_tasks` parameters are fixed in the `config.yml` file.

```shell
embulk -J-Xms1024m -J-Xmx1024m run config.yml
```

<img width="1474" alt="スクリーンショット 2023-11-22 12 09 00" src="https://github.com/gtnao0219/embulk-memory-leak-debug/assets/25474324/9b89b0d7-733e-407b-93da-a48cd0e92185">
