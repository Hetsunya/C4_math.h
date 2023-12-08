#!/bin/bash
FLAGS=-Wall -Wextra
CC=gcc -lm
FUNC_FILES_C=*.c
FUNC_FILES_O=*.o
CHECKFLAGS=$(shell pkg-config --cflags --libs check)
GCOVFLAGS=-fprofile-arcs -ftest-coverage
LIBNAME=s21_math.a
GLFLAGS=--coverage
GCOVFLAGS=-fprofile-arcs -ftest-coverage
sourceFilesArray=$(ls sourceFiles)

all: s21_math.a

build_object_files:
	$(CC) $(FLAGS) -c $(FUNC_FILES_C)

build_library:
	ar rcs $(LIBNAME) $(FUNC_FILES_O)

s21_math.a: build_object_files
# 	cp tests/s21_math.h s21_math.h
	make build_library
	rm -rf *.o

test: s21_math.a
	$(CC) s21_test_abs.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_abs
	$(CC) s21_test_acos.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_acos
	$(CC) 	s21_test_asin.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_asin
	$(CC) s21_test_atan.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_atan
	$(CC) s21_test_ceil.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_ceil
	$(CC) s21_test_cos.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_cos
	$(CC) s21_test_exp.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_exp
	$(CC) s21_test_fabs.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_fabs
	$(CC) s21_test_floor.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_floor
	$(CC) s21_test_fmod.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_fmod
	$(CC) s21_test_log.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_log
	$(CC) s21_test_pow.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_pow
	$(CC) s21_test_sin.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_sin
	$(CC) s21_test_sqrt.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_sqrt
	$(CC) s21_test_tan.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) $(GCOVFLAGS) -o s21_test_tan

	make start_tests

make clean_tests:
	rm -rf s21_test*

start_tests:
	./s21_test_acos
	./s21_test_asin
	./s21_test_cos
	./s21_test_log
	./s21_test_exp
	./s21_test_abs
	./s21_test_pow
	./s21_test_ceil
	./s21_test_atan
	./s21_test_fabs
	./s21_test_floor
	./s21_test_fmod
	./s21_test_sin
	./s21_test_sqrt
	./s21_test_tan

gcov_report: clean build_object_files build_library test
# 	gcov $(FUNC_FILES_C)
#	pip install git+https://github.com/gcovr/gcovr.git
	~/.local/bin/gcovr -r . --html --html-details -o s21_math.html

gcov_html: st gcov_report
	xdg-open s21_math.html

clean:
	rm -rf *.o
	rm -rf *.gcno
	rm -rf *.gcov
	rm -rf *.gcda
	rm -rf *.a
# 	rm -rf s21*

rebuild: clean all
