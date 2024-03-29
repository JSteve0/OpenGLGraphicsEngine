########################################################
# Makefile for CSCI 375
#   In many cases you will ONLY need to modify the
#   SRCS variable below
# Author: Gary M. Zoppetti, Ph.D. Chad Hogg, and
# 	      Justin Stevens
########################################################

########################################################
# Variable definitions
########################################################
# C++ compiler
CXX := g++
#CXX := clang++

# Include directories, prefaced with "-I"
INCDIRS  := -isystem /usr/include/catch2

# C++ compiler flags
# Use the first for debugging, the second for release
#CXXFLAGS := -g -Wall -std=c++14 $(INCDIRS)
CXXFLAGS := -O3 -Wall -std=c++14 $(INCDIRS)

# Linker. For C++ should be $(CXX).
LINK := $(CXX)

# Linker flags. Usually none.
LDFLAGS := 

# Library paths, prefaced with "-L". Usually none.
LDPATHS := 

UNAME := $(shell uname)
# Libraries used, prefaced with "-l".
ifeq ($(UNAME),Darwin)
LDLIBS := -framework OpenGL -lGLEW -lglfw -lassimp -lfreeimage
else
LDLIBS := -lGLEW -lglfw -lGL -lassimp -lfreeimage
endif

# All source files, separated by spaces. Don't include header files. 
SRCS := Main.cpp ShaderProgram.cpp OpenGLContext.cpp RealOpenGLContext.cpp Mesh.cpp Scenes/Scene.cpp Scenes/MyScene.cpp Camera.cpp Vector3.cpp KeyBuffer.cpp Matrix3.cpp Transform.cpp MouseBuffer.cpp Vector4.cpp Matrix4.cpp Geometry.cpp NormalsMesh.cpp ColorsMesh.cpp LightSource.cpp Material.cpp Texture.cpp TexturedNormalsMesh.cpp Scenes/PhysicsScene.cpp PhysicsObject.cpp Scenes/Pong2DScene.cpp Scenes/Pong2DScene2P.cpp Scenes/Pong/Ball.cpp Scenes/Pong/Player.cpp Scenes/Pong/AI.cpp

# Extension for source files. Do NOT modify.
SOURCESUFFIX := cpp

# Determines object files based on SRCS.
OBJS := $(SRCS:.$(SOURCESUFFIX)=.o)

# Executable name. Defaults to basename of first name in SRCS.
EXEC := $(patsubst %.o, %, $(word 1, $(OBJS))).out

# Command to generate dependency rules for make. 
MAKEDEPEND := $(CXX) $(CPPFLAGS) $(CXXFLAGS) -MM -MP

# The name of the AutoLab course we will submit to.
COURSE := 375-s22

# The name of the current assignment.
ASSIGNMENT := a09project

#############################################################
# Rules
#   Rules have the form
#   target : prerequisites
#   	  recipe
#############################################################

all : $(EXEC)

$(EXEC) : $(OBJS)
	$(LINK) $(LDFLAGS) $(LDPATHS) $^ -o $@ $(LDLIBS)

-include Makefile.deps

#############################################################

.PHONY : clean submit handin.zip

handin.zip :
	zip -r handin.zip * --exclude handin.zip Makefile.deps \*.o \*.out \*~

submit : handin.zip
	git tag $(ASSIGNMENT) -f -m "Final submission of $(ASSIGNMENT)."
	git push --tags -f
	autolab submit $(COURSE):$(ASSIGNMENT) handin.zip

TestVector3.out : TestVector3.cpp Vector3.cpp Vector3.hpp
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -o TestVector3.out TestVector3.cpp Vector3.cpp

TestMatrix3.out : TestMatrix3.cpp Vector3.cpp Vector3.hpp Matrix3.cpp Matrix3.hpp
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) -o TestMatrix3.out TestMatrix3.cpp Vector3.cpp Matrix3.cpp

clean :
	$(RM) $(EXEC) $(OBJS) a.out core
	$(RM) Makefile.deps *~

.PHONY :  Makefile.deps
Makefile.deps :
	$(MAKEDEPEND) $(SRCS) > $@

#############################################################
#############################################################
