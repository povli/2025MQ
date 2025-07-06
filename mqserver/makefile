# -------- 目录 --------
MUDUO_ROOT  := ../tools/muduo/_install
MUDUO_INC   := $(MUDUO_ROOT)/include
MUDUO_LIB   := $(MUDUO_ROOT)/lib
EXAMPLE_INC := ../tools/muduo/examples
TOOLS_ROOT  := ../tools                 # << 新增
SRC_INC     := ../tools/muduo/muduo 

# -------- 编译 / 链接 --------
CXX      := g++
CXXFLAGS := -g -std=c++11 -Wall -I$(MUDUO_INC) -I$(EXAMPLE_INC) -I$(TOOLS_ROOT) -I$(SRC_INC)
LDFLAGS  := -L$(MUDUO_LIB) \
            -lmuduo_net -lmuduo_base \
            -lprotobuf -lsqlite3 -lgtest -lpthread -lz

# -------- 源文件 --------
SRCS := server.cc \
        $(wildcard ../mqcommon/*.cc) \
        ../tools/muduo/examples/protobuf/codec/codec.cc

OBJS   := $(SRCS:.cc=.o)
TARGET := server

# -------- 规则 --------
$(TARGET): $(OBJS)
	$(CXX) $(OBJS) -o $@ $(LDFLAGS)

%.o: %.cc
	$(CXX) $(CXXFLAGS) -c $< -o $@

.PHONY: clean
clean:
	rm -f $(OBJS) $(TARGET)
	rm -rf data/ log/
