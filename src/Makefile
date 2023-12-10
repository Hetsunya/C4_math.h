#!/bin/bash
FLAGS=-Wall -Wextra -Werror
CC=gcc -lm
FUNC_FILES_C=sourceFiles/*.c
FUNC_FILES_O=*.o
CHECKFLAGS=$(shell pkg-config --cflags --libs check)
GCOVFLAGS=-fprofile-arcs -ftest-coverage
LIBNAME=s21_math.a
GLFLAGS=--coverage
sourceFilesArray=$(ls sourceFiles)


peer: gcov_report gcov_html

all: s21_math.a

build_object_files:
	$(CC) $(FLAGS) $(GCOVFLAGS) $(GLFLAGS) -c $(FUNC_FILES_C)

build_library:
	ar rcs $(LIBNAME) $(FUNC_FILES_O)

s21_math.a: build_object_files
# 	cp tests/s21_math.h s21_math.h
	make build_library
	rm -rf *.o

test: s21_math.a
	$(CC) tests/s21_test_abs.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_abs
	$(CC) tests/s21_test_acos.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_acos
	$(CC) tests/s21_test_asin.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_asin
	$(CC) tests/s21_test_atan.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_atan
	$(CC) tests/s21_test_ceil.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_ceil
	$(CC) tests/s21_test_cos.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_cos
	$(CC) tests/s21_test_exp.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_exp
	$(CC) tests/s21_test_fabs.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_fabs
	$(CC) tests/s21_test_floor.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_floor
	$(CC) tests/s21_test_fmod.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_fmod
	$(CC) tests/s21_test_log.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_log
	$(CC) tests/s21_test_pow.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_pow
	$(CC) tests/s21_test_sin.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_sin
	$(CC) tests/s21_test_sqrt.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_sqrt
	$(CC) tests/s21_test_tan.c -L. s21_math.a $(CHECKFLAGS) $(GLFLAGS) -o s21_test_tan

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
# 	gcov -o $(FUNC_FILES_C)
	gcov *.gcno
	gcov *.gcda
#	pip install git+https://github.com/gcovr/gcovr.git
	~/.local/bin/gcovr -r . --html --html-details -o s21_math.html --exclude 'tests/.*'

gcov_html:
	xdg-open s21_math.html

clean:
	rm -rf *.o
	rm -rf *.gcno
	rm -rf *.gcov
	rm -rf *.gcda
	rm -rf *.a
	rm -rf s21*

rebuild: clean all
