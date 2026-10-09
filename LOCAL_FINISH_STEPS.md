# Local finish steps (run in VS Code terminal from assignment root)

The supplied outputs passed the bundled local checker (100/100) in a separate environment. The bundled `output/environment.txt` records that environment, not your computer, and **must be regenerated locally**. The required NumPy 2.3.3 installation could not be performed in the isolated build environment because PyPI was unreachable.

1. Make sure you are working inside your cloned assignment fork, and copy the provided files into it (keep the folder structure). Do not replace your `.git` directory.
2. Run the README's environment commands:

```bash
uv python pin 3.13
uv venv --seed
source .venv/bin/activate
uv sync
```

3. Recreate the environment report from your active environment:

```bash
mkdir -p output
echo "python: $(python3 --version)" > output/environment.txt
echo "numpy: $(python3 -c 'import numpy as np; print(np.__version__)')" >> output/environment.txt
echo "interpreter: $(python3 -c 'import sys; print(sys.executable)')" >> output/environment.txt
```

4. Regenerate the shell artifacts, using the required shell pipelines:

```bash
tail -n +2 data/bp_readings.csv | wc -l > output/record_count.txt
timestamp=$(date +%Y%m%d_%H%M%S)
tail -n +2 data/bp_readings.csv | cut -d, -f2 | sort | uniq -c > "output/monitor_counts_${timestamp}.txt"
```

5. Run the program and local grader:

```bash
python3 analysis.py
python3 check_assignment.py
```

6. Confirm the interpreter path in `output/environment.txt` points inside your project's `.venv`, commit `.python-version`, `analysis.py`, and `output/` files, push, and verify the GitHub Actions run succeeds. The GitHub workflow was not executed in this isolated build environment.

The grader reads output artifacts rather than checking whether the required shell commands were used, so the commands above document and reproduce the required Task 2 method.
