# Introduction to Parallel

[GNU Parallel](https://www.gnu.org/software/parallel/){:target="_blank" rel="noopener"} is a shell tool that allows for independent jobs to be run in parallel over multiple compute resources. 

## Bash Loop Using Parallel

[GNU Parallel](https://www.gnu.org/software/parallel/){:target="_blank" rel="noopener"} can greatly speed up a task given that it can leverage multiple compute resources at once. Let's examine the case of the following bash loop (example taken from [Yale Center For Research Computing - Parallel](https://docs.ycrc.yale.edu/clusters-at-yale/guides/parallel/)):

```bash
for letter in {a..f};
do
    echo $letter
done
```

!!! info "output"

    ```bash
    a
    b
    c
    d
    e
    f
    ```

To par
## References

1.
2.  https://docs.ycrc.yale.edu/clusters-at-yale/guides/parallel/
