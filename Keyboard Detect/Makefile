NAME = keyboard

CC = cc

CFLAGS = -Wall -Werror -Wextra

LIB_MLX = ./mlx/libmlx.a

SRC = keyboard-detect.c

RM = rm -rf

OS := $(shell uname) 

OBJ = $(SRC:.c=.o)

ifeq ($(OS), Darwin)
	MLXFLAGS = -lm -lXext -lX11
else
	MLXFLAGS = -framework OpenGL -framework AppKit
endif

all: $(NAME)
	@echo "compile done!"

$(NAME): $(OBJ) $(LIB_MLX)
	$(CC) $(CFLAGS) -I./mlx $(LIB_MLX) $(MLXFLAGS) $(OBJ) -o $(NAME)

$(LIB_MLX):
ifeq ($(OS), Darwin)
	curl https://projects.intra.42.fr/uploads/document/document/12154/minilibx-linux.tgz -o mlx.tgz
	tar -xf mlx.tgz
	$(RM) mlx.tgz
	mv ./minilibx-linux ./mlx
	make -C ./mlx
else
	curl https://projects.intra.42.fr/uploads/document/document/12900/minilibx_opengl.tgz -o mlx.tgz
	tar -xf mlx.tgz
	$(RM) mlx.tgz
	mv ./minilibx_opengl_20191021 ./mlx
	make -C ./mlx
endif


clean:
	$(RM) $(OBJ)
	@if [ -d Mlx ] ; then \
		make clean -C Mlx ; \
	fi

fclean: clean
	$(RM) $(NAME)
	$(RM) ./mlx

re: fclean all

.PHONY = all clean fclean re
