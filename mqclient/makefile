###############################################################################
# 目录配置 —— 若 Muduo 安装目录位置变化，只改这三行即可
###############################################################################
MUDUO_INSTALL := ../tools/muduo/_install
MUDUO_SRCROOT := ../tools/muduo
EXAMPLE_DIR   := ../tools/muduo/examples                # codec.h/dispatcher.h
TOOLS_ROOT  := ../tools 

###############################################################################
# 编译 / 链接选项
###############################################################################
CXX      := g++
CXXFLAGS := -g -std=c++11 -Wall \
            -I$(MUDUO_INSTALL)/include \
            -I$(EXAMPLE_DIR) \
            -I$(MUDUO_SRCROOT) \
			-I$(TOOLS_ROOT)

LDFLAGS  := -L$(MUDUO_INSTALL)/lib \
            -lmuduo_net -lmuduo_base \
            -lprotobuf -lsqlite3 -lgtest -lpthread -lz

###############################################################################
# 公共源文件列表（自动展开）
###############################################################################
COMMON_SRCS := $(wildcard ../mqcommon/*.cc) \
               ../tools/muduo/examples/protobuf/codec/codec.cc

###############################################################################
# 生成三个可执行文件
###############################################################################
TARGETS := publish_client consume_client client

all: $(TARGETS)

# 单独指定每个目标自身的主文件
publish_client: SRCS := publish_client.cc   $(COMMON_SRCS)
consume_client: SRCS := consume_client.cc   $(COMMON_SRCS)
client:         SRCS := client.cc           $(COMMON_SRCS)

# 通用规则 —— $@ 为目标名
$(TARGETS):
	$(CXX) $(CXXFLAGS) $(SRCS) -o $@ $(LDFLAGS)

###############################################################################
# 清理
###############################################################################
.PHONY: clean all
clean:
	rm -f $(TARGETS) *.o ../mqcommon/*.o
	rm -rf log
