# anna-dl
Python tool allowing easy books downloads from the terminal

Replacement for [zlib-dl](https://github.com/Nquxii/zlib-dl)

<img src="images/demo-f.gif" align="center">

## Features
- Bypass randomly generated links to downloads
- Obtain a specified number of results
- Search multiple configured sources and group duplicate results by MD5
- Try alternative source URLs when a download fails
- Automatically try Google Chrome, then Chromium

## Installation
Clone the repository and install dependencies
```
git clone https://github.com/Nquxii/anna-dl
cd anna-dl
```
```
pip3 install -r requirements.in
```

Open help section
```
python3 annadl --help
```

Ensure your config.json is set if you don't want to use several parameters each time.

Add annadl to path (so you don't need to cd into zlib-dl every time) Linux/MacOS:
```
ln -s ~[CURRENT DIR]/annadl ~/.local/bin/annadl
```

## Usage
```
python3 annadl [path] --s [query] --n [number of results]
```
Number of results defaults to 5 of the top unique results available. Use 0 to see all unique results.

Options:

- `--s QUERY` — required search query.
- `--n NUMBER` — maximum number of unique results; `0` means all results.
- `--all` — attempt to download every unique result, continuing after failures.
- `path` — optional download directory; defaults to `download_path` in `config.json`, then `./assets/`.

Use `--all` to attempt downloading every result returned by the search. If a
download fails, the tool continues with the next result and prints a summary
of failures at the end.

The tool automatically tries Google Chrome first and Chromium second. It
checks PATH and common Windows installation directories, so no browser choice
is required on the command line.

Search sources are configured in `config.json`. Each source should be a base
URL; results with the same MD5 are grouped together and their source URLs are
tried in order:

```json
{
    "download_path": "",
    "search_urls": [
        "https://annas-archive.gl",
        "https://another-mirror.example"
    ]
}
```


If a path in the command is specified, it will be used. Otherwise, the download_path in config.json will be used.
If none of these options are available, the program will use `./assets/` as its download folder.

### Example
View 5 search results for "The Pragmatic Programmer". Download the resulting file in /home/johndoe/Documents/books
```
python3 annadl /home/johndoe/Documents/books --s "The Pragmatic Programmer"
```

View **all** search results on the first page for "Don Quixote". Download the resulting file in ./assets/ (assuming no set path in config.json)
```
python3 annadl --s "Don Quixote" --n 0
```
