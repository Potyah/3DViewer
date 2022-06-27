.PHONY: all clean tests dvi install uninstall dist
XX=g++
APP=$(BD)3D_Viewer2_1.app

FILES= Model/s21_matrix_oop.cpp \
	   Model/affineTransformations.cpp \

DIRS= View \
	  Model \
	  Controller \
	  Icon \
	  giflib \
	  doc \

LDFLAGS= -Wall -Wextra -Werror -std=c++17 -g
OS := $(shell uname -s)
TEST_FLAGS= -lgtest -lgtest_main -lpthread
BD= build/

ifeq ($(OS), Darwin)
	CC += -D OS_MAC
else
	CC += -D OS_LINUX
endif

all: build install tests

build: clean copy
	cd $(BD); qmake 3D_Viewer2_1.pro
	make -C $(BD)

copy:
	@mkdir build
	cp *.pro *.cpp *.qrc $(BD)
	rsync -rupE $(DIRS) $(BD)

install: uninstall build
	@mkdir $(HOME)/Applications/3D_Viewer2_1/ 2>/dev/null
	cp -rf $(APP) $(HOME)/Applications/3D_Viewer2_1/
	make clean

uninstall: 
	rm -rf $(HOME)/Applications/3D_Viewer2_1

dist:
	rm -rf 3D_Viewer2_1
	mkdir 3D_Viewer2_1
	cp Makefile *.pro *.cpp 3D_Viewer2_1/
	rsync -rupE $(DIRS)  3D_Viewer2_1/
	tar -cvzf $(HOME)/Desktop/3D_Viewer2_1.tgz 3D_Viewer2_1/
	rm -rf 3D_Viewer2_1/

dvi:
	open doc/index.html

tests: clean
	$(XX) $(LDFLAGS) $(FLAGS) Tests/3DViwerTests.cpp $(FILES) -lstdc++ $(TEST_FLAGS) -o test
	./test

clean:
	rm -rf build test *.a *.o *.cfg *.gcda *.gcno *.html *.info *.dSYM report
