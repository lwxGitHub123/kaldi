all: ;

EXTRA_CXXFLAGS = -Wno-sign-compare
include ../kaldi.mk

ifeq ($(IS_GPU_BUILD), true)
ifeq ($(WITH_CUDADECODER), true)

# Make sure we have CUDA_ARCH from kaldi.mk,
ifeq ($(CUDA), true)
  ifndef CUDA_ARCH
    $(error CUDA_ARCH is undefined, run 'src/configure')
  endif
endif

LDFLAGS += $(CUDA_LDFLAGS)
LDLIBS += $(CUDA_LDLIBS)

BINFILES = compute-mfcc-feats-cuda \
           compute-online-feats-cuda \
           compute-fbank-feats-cuda \
           apply-batched-cmvn-online-cuda \
           compute-mfcc-online-batched-cuda \
           compute-fbank-online-batched-cuda \
           compute-online-feats-batched-cuda

OBJFILES =

TESTFILES =

ADDLIBS = ../cudafeat/kaldi-cudafeat.a ../online2/kaldi-online2.a  \
          ../ivector/kaldi-ivector.a ../decoder/kaldi-decoder.a \
          ../lat/kaldi-lat.a ../cudamatrix/kaldi-cudamatrix.a \
          ../hmm/kaldi-hmm.a ../feat/kaldi-feat.a \
          ../transform/kaldi-transform.a ../gmm/kaldi-gmm.a \
          ../tree/kaldi-tree.a ../util/kaldi-util.a ../matrix/kaldi-matrix.a \
          ../base/kaldi-base.a

else
all:
	$(warning "Not building cudadecoder extension -- to build with it, configure with --with-cudadecoder[=true]")
endif

endif

include ../makefiles/default_rules.mk
