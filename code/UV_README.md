Using `uv` for package management

- Install all dependencies listed in `requirements.txt`:

```bash
pip install -r code/requirements.txt
```

- `uv` is included in `requirements.txt`; to install it explicitly:

```bash
pip install uv
```

- To run the web app (development server):

```bash
python code/scanner.py
```

- For `uv` usage, run `uv --help` to see available commands. If you want, I can demonstrate adding/removing packages with `uv` once you confirm it's the right tool.
