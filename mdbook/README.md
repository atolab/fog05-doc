

The Eclipse fog05 user guide has been written in Markdown using `mdbook` rust template to generate the online book-like website you can read.

To build the Eclipse fog05 user guide:

1. Install mdbook:

```bash
$ cargo install mdbook
```

The previous command will download and compile mdBook for you.

2. Usage

``` bash
$ mdbook build
```

This is the command you will run to render your book, it reads the `SUMMARY.md` file to understand the structure of your book, takes the markdown files in the source directory as input and outputs static html pages that you can upload to a server.


3. Output

The output of the build is located in the `book` folder. To visualized the result do:

```bash
$ mdbook serve
```

and visit the following url:

http://localhost:3000
