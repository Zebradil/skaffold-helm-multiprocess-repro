# Reproduction of a skaffold bug when rendering a helm chart in multiple processes

## Steps to reproduce

```shell
# Run 50 instances of skaffold render in parallel
for i in {1..50}; do skaffold render --offline 2>err/$i.log >/dev/null & ; done

# Wait for all processes to finish
wait

# Check for files with errors in `err` directory
cat err/*.log

# If there are no errors, repeat the steps above
```

Example result is checked in in the `err` directory.
Different errors are possible, but the most frequent one is the following:

```
std out err: %!(EXTRA *errors.errorString=Error: lstat /private/var/folders/w4/nsbl5rq524b1r2w_jzh2q45m0000gp/T/tmp.B8ITfAHBHc/foo/tmpcharts-83163: no such file or directory
)
```
