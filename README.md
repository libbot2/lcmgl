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


### License:

lcmgl is free software: you can redistribute it and/or modify it under the
terms of the GNU Lesser General Public License as published by the Free
Software Foundation, either version 3 of the License, or (at your option) any
later version.

lcmgl is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU Lesser General Public License for more
details.

You should have received a copy of the GNU Lesser General Public License along
with lcmgl. If not, see <http://www.gnu.org/licenses/>.
