# SPDX-License-Identifier: GPL-2.0
#
# Copyright (C) 2015-2017 Jason A. Donenfeld <Jason@zx2c4.com>. All Rights Reserved.

ccflags-y := -O3 -fvisibility=hidden
ccflags-$(CONFIG_WIREGUARD_DEBUG) += -DDEBUG -g
ccflags-y += -Wframe-larger-than=8192
ccflags-y += -D'pr_fmt(fmt)=KBUILD_MODNAME ": " fmt'
wireguard-y := main.o noise.o device.o peer.o timers.o queueing.o send.o receive.o socket.o hashtables.o allowedips.o ratelimiter.o cookie.o netlink.o
wireguard-y += crypto/curve25519.o crypto/chacha20poly1305.o crypto/blake2s.o

wireguard-$(CONFIG_X86_64) += crypto/chacha20-x86_64.o crypto/poly1305-x86_64.o crypto/blake2s-x86_64.o crypto/curve25519-x86_64.o
wireguard-$(CONFIG_ARM) += crypto/chacha20-arm.o crypto/poly1305-arm.o crypto/curve25519-arm.o
wireguard-$(CONFIG_ARM64) += crypto/chacha20-arm64.o crypto/poly1305-arm64.o
wireguard-$(if $(filter yy,$(CONFIG_MIPS)$(CONFIG_64BIT)),y,n) += crypto/poly1305-mips64.o

include $(src)/compat/Makefile.include

obj-$(if $(KBUILD_EXTMOD),m,$(CONFIG_WIREGUARD)) := wireguard.o
