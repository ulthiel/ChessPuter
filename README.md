# ChessPuter
ChessPuter (chess pyoo-ter) is a UCI (Universal Chess Interface) compatible** command line chess playing program written in C++.

ChessPuter can be compiled on Linux with its Makefile. It can be installed and played with best on PyChess (https://github.com/pychess/pychess).

** ChessPuter is not yet fully UCI compatible. To be fully compatible, the following changes still need to be made:
  - The use of threads must be implemented to allow the program to immediately respond to commands such as "stop", "isready", and others.
  - The command string processing should be made to be case-insensitive.

## Fixes by UT

I have fixed a little problem that I noticed when using ChessPuter with Polyglot and an opening book:

```
uci
id name ChessPuter
id author Miles Bright
uciok
ucinewgame
position startpos moves d2d4 d7d5
go
bestmove d2d4
```

This is of course an illegal move. The problem is that there is a ```firstMove``` bool which is not set to false by the position command and then the engine always makes the d2d4 move, no matter what the actual board state is. I've fixed this:

```
uci
id name ChessPuter (Feb18, UT fix)
id author Miles Bright
uciok
ucinewgame
position startpos moves d2d4 d7d5
go
bestmove g1f3
```

Moreover, I've added a ```compile-mac.sh``` script because the compilation didn't work on macOS.