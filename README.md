# minishell: a C-based shell that mimics bash

**minishell** is my ninth Codam project and a very defining project for me and all Codam students. This is the first group project and the first really big project that took half a year to finish. Minishell is unique because it consists of so many parts; it requires a deep understanding of the bash terminal and many different coding concepts. Proper parsing, memory management, and writing readable code were essential to finishing this project after multiple rewrites of parsing, expanding, and executing. For this project, my project partner and I also introduced **vector** as a datatype in C, which led to a better understanding of memory management.

##### The project is stored on my project partner's GitHub:
[View the minishell project on GitHub](https://github.com/lithiumox-codam/minishell/tree/main/src)

## Project Highlights

- **First large project**: This was my first large project that involved setting up a good data flow so different parts could be tested and developed separately.
- **Understanding bash**: We implemented heredoc, redirects, executing programs with parameters, and a couple of built-ins. To have these function in a similar fashion to bash, we needed to learn how bash handles all of these aspects.
- **Introducing vectors to C**: Because of the complex parsing involved with the terminal, we introduced vectors to have easy insertions & deletions, random access by iterator, and more robust code.

## The project

In order to work as a team, we separated minishell into many different parts, each part needed to take input from the previous part and provide its own proper output.

- **parser**: Reads the input from the stdin and puts it into the vector, separating the parts based on whitespace and tokens. Transforming
```
<<endl readhere.exe|grep -e $USER| useoutput.exe>outfile.txt
```
transforms into:

| Token         | Description          |
|---------------|----------------------|
| `<<`          | Here-document        |
| `endl`        | End of here-doc      |
| `readhere.exe`| Executable           |
| `\|`          | Pipe                 |
| `grep`        | Command              |
| `-e`          | Option for grep      |
| `$USER`       | Environment variable |
| `\|`          | Pipe                 |
| `useoutput.exe`| Executable          |
| `>`           | Redirect             |
| `outfile.txt` | Output file          |

- **lexer**: The lexer identifies all of these parts and marks tokens as such.

- **expander**: The expander expands the environment variables into strings, utilizing a *char *string* vector.

- **group**: Groups the different pipes into their individual processes.

- **exec**: The executor, executes the programs called and writes to the appropriate output files.

- **built_in**: The built-in programs such as `echo`, `pwd`, and `env`.

- **signals**: Handles signals called during the running of minishell.

### Vectors

Before starting the project, we wanted to introduce a useful datatype to C for storing and expanding the information of minishell. Mees came up with using vectors that we know from other programming languages such as C++. Of course, vectors don't exist in C, so we made our own. Vectors brought many advantages compared to a linked-list.

Our vector library (found in libft) works by the following concepts:

- **Ease of use**: We wanted all of our project parts to easily be able to access, insert, and delete the required data.
- **Memory safety**: The `vector` handles the memory. Once a string is added to the vector, cleaning it up is up to the vector. At the end of the program, we call `vec_free`, which frees all components of the vector. The free function for each specific component is provided to the vector at initialization.
- **Consistency**: The vector library allows us to consistently only use this datatype, making the entire code base easy to read.
- **Versatility**: `vector` can store any memory-allocated data, which means you can store any struct of varying sizes. With the condition that you provide the right cleanup function, the vector is entirely memory safe.

## Conclusion

This was a really fun project to work on as it was a great learning opportunity for good project architecture design. Writing robust code, documenting what all your main functions do, and thinking about what data you input and provide to the next part were really useful and have remained great coding tools in all my projects after this.

Feel free to use all the code on the provided GitHub page; the project is meant for learning!