CC ?= gcc

CFLAGS	= -std=c11 -Wall -Wextra -Wpedantic -Werror -g
# 注意需要指定 -static
LDFLAGS = -static

OUTPUT_DIR ?= .

SRCS		= main.c functions.c
OBJS		= $(SRCS:.c=.o)
TARGET		= $(OUTPUT_DIR)/exercise-03

TEST_SRCS	= test.c functions.c
TEST_OBJS	= $(TEST_SRCS:.c=.o)
TEST_TARGET = $(OUTPUT_DIR)/exercise-03_test

all: $(TARGET)

$(TARGET): $(OBJS) $(LIB_OBJS)
	$(CC) $(LDFLAGS) -o $@ $^

$(TEST_TARGET): $(TEST_OBJS) $(LIB_OBJS)
	$(CC) $(LDFLAGS) -o $@ $^

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

%.a: %.c
	$(CC) $(CFLAGS) -c $< -o $@
	ar rcs $@ $@

test: $(TEST_TARGET)
	./$(TEST_TARGET)

clean:
	rm -f $(TARGET) $(TEST_TARGET) $(OBJS) $(TEST_OBJS)
