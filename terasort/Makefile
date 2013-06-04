include ../Makefile.env
CFLAGS+=-std=c99 -g

LDFLAGS+=-lmapreduce -lnetworking

all: createdirs clean map.nexe reduce.nexe gensort
	./gendatamanifest.sh

map.nexe: obj/map.o obj/user_implem.o
	@$(CC) -o map.nexe obj/map.o obj/user_implem.o $(LDFLAGS)

reduce.nexe: obj/reduce.o obj/user_implem.o
	@$(CC) -o reduce.nexe obj/reduce.o obj/user_implem.o $(LDFLAGS)

obj/map.o: src/map.c
	@$(CC) -c -o obj/map.o ${CFLAGS} src/map.c

obj/reduce.o: src/reduce.c
	@$(CC) -c -o obj/reduce.o ${CFLAGS} src/reduce.c

obj/user_implem.o: src/user_implem.c src/user_implem.h
	@$(CC) -c -o obj/user_implem.o ${CFLAGS} src/user_implem.c -D_GNU_SOURCE

createdirs:
	chmod u+rwx gendatamanifest.sh start.sh
	@mkdir -p obj log data

gensort:
	if test ! -d gensort-1.5 ; then \
		tar xf gensort-1.5.tar.gz ;\
	fi
	$(MAKE) -C gensort-1.5

clean: 
	@rm -f obj/*.o
	@rm -f log/*.log
	@rm -f data/*.txt
	@rm -f data/*.dat
	@rm -f data/*.sum
	@rm -f manifest/*.manifest	
	@rm -f *.nexe
	@rm -f nameservice.log

