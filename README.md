# bot2-lcmgl

Transmit OpenGL commands over LCM, and render them elsewhere.

### Description:

bot2-lcmgl contains a set of client libraries in C, Java, and Python for
transmitting OpenGL commands over LCM. It also provides routines for receiving
and rendering these commands in either a standalone application
(`bot-lcmgl-viewer`), or incorporated into another C/C++ application.

A nice attribute of the client libraries is that they do not depend on any
OpenGL libraries, and only require LCM.

### Dependencies:

Required:

- CMake (2.8.12 or later)
- LCM (1.4.0 or later)
- GTK+ (2.0 or later)
- OpenGL
- GLUT / FreeGLUT
- ZLib

Optional:

- Java
- Python
