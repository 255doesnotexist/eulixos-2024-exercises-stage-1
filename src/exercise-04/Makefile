CC ?= gcc

CFLAGS	= -std=c11 -Wall -Wextra -Wpedantic -Werror -g
LDFLAGS = -Wl,--as-needed -Wl,--no-undefined

OUTPUT_DIR ?= .

SRCS		= main.c
OBJS		= $(SRCS:.c=.o)
TARGET		= $(OUTPUT_DIR)/exercise-04

LIB_NAME	= libfunctions.a
LIB_TARGET	= $(OUTPUT_DIR)/$(LIB_NAME)
LIB_SRC		= functions.c
LIB_OBJ		= $(LIB_SRC:.c=.o)

TEST_SRCS	= test.c functions.c
TEST_OBJS	= $(TEST_SRCS:.c=.o)
TEST_TARGET = $(OUTPUT_DIR)/exercise-04_test

all: $(TARGET) test

$(OUTPUT_DIR):
	mkdir -p $(OUTPUT_DIR)

$(LIB_OBJ): $(LIB_SRC) | $(OUTPUT_DIR)
	# 在这里指定如何编译 functions.o
	$(CC) $(CFLAGS) -c $< -o $@

$(LIB_TARGET): $(LIB_OBJ) | $(OUTPUT_DIR)
	# 在这里指定如何生成静态链接库
	ar rcs $@ $^
	ranlib $@

$(TARGET): $(OBJS) $(LIB_TARGET) | $(OUTPUT_DIR)
	# 在这里指定如何链接 libfunctions.a 来生成 TARGET
	$(CC) $(LDFLAGS) -o $@ $(OBJS) $(LIB_TARGET)

$(TEST_TARGET): $(TEST_OBJS) $(LIB_TARGET) | $(OUTPUT_DIR)
	# 在这里指定如何链接 libfunctions.a 来生成 TEST_TARGET
	$(CC) $(LDFLAGS) -o $@ $(TEST_OBJS) $(LIB_TARGET)

%.o: %.c
	# 在这里指定所有 C 文件的编译命令
	$(CC) $(CFLAGS) -c $< -o $@

test: $(TEST_TARGET)
	$(TEST_TARGET)

clean:
	rm -f $(LIB_TARGET) $(TARGET) $(TEST_TARGET) $(OBJS) $(LIB_OBJ) $(TEST_OBJS)
