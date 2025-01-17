TRACE=
ifeq ($(TRACE), true)
override OTHERFLAGS += --trace_error --prn
endif
PRN=
ifeq ($(PRN), true)
override OTHERFLAGS += --prn
endif

FSTAR=../../bin/FStar.exe --fstar_home ../../ $(OTHERFLAGS)

ALLFILES=utils list tuple rec pat letrec termination skel 

%.tc: %.fst
	$(FSTAR) --pretype --prims prims.fst $^

bug:
	$(FSTAR) --pretype --prims prims.fst dsenv.fsi

prims: 
	$(FSTAR) --pretype --prims prims.fst 

utils:
	$(FSTAR) --pretype --codegen OCaml --prims prims.fst utils.fst

list:
	$(FSTAR) --pretype --codegen OCaml  --prims prims.fst list.fst


STDFILES=list.fst option.fst string.fst 
BASICFILES=bytes.fst util.fst getoptsimple.fst options.fs range.fst unionfind.fst
BASIC=$(addprefix ../../src/basic/, $(BASICFILES))
SYNTAXFILES=syntax.fs const.fs visit.fs util.fs print.fs
SYNTAX=$(addprefix ../../src/absyn/, $(SYNTAXFILES))
PARSERFILES=ast.fs dsenv.fsi dsenv.fs desugar.fsi desugar.fs parse.fst lexhelp.fs parseit.fst driver.fs 
PARSER=$(addprefix ../../src/parser/, $(PARSERFILES))
TCFILES=errors.fs tcenv.fsi tcenv.fs normalize.fsi normalize.fs rel.fsi rel.fs tcutil.fsi tcutil.fs tc.fs
TC=$(addprefix ../../src/tc/, $(TCFILES))
FORMATFILES=format.fsi format.fs
FORMAT=$(addprefix ../../src/format/, $(FORMATFILES))
BACKENDFILES=nameenv.fsi nameenv.fs syntax.fs ocaml-asttrans.fsi ocaml-asttrans.fs ocaml-codegen.fsi ocaml-codegen.fs oaml.fsi ocaml.fs
BACKEND=ocaml-backend-stub.fst
MAINFILES=fstar.fs
MAIN=$(addprefix ../../src/, $(MAINFILES))

ALL=st.fst $(STDFILES) $(BASIC) $(SYNTAX) $(PARSER) $(TC) backends.fsi $(BACKEND) 
#$(MAIN)

pt-compiler:
	$(FSTAR) --pretype --prims prims.fst $(ALL)


compiler:
	$(FSTAR) --prims prims.fst $(STDFILES) $(BASIC) $(SYNTAX) $(PARSER) $(TC) backends.fsi $(MAIN)


wc: prims.fst $(ALL)

# # Change the following line to the location of the top MITLS directory "lang-sec/msrc/cvk/samples/protocols/tls"
MITLS=../../../mitls/

PDIR=$(MITLS)ML/Platform/
PLATFORM=$(PDIR)Bytes.fst $(PDIR)Date.fst $(PDIR)Error.fst $(PDIR)Tcp.fst

CDIR=$(MITLS)ML/CoreCrypto/
CRYPTO=$(CDIR)CoreKeys.fst $(CDIR)CoreACiphers.fst $(CDIR)CoreHMac.fst $(CDIR)CoreRandom.fst $(CDIR)CoreCiphers.fst $(CDIR)CoreHash.fst $(CDIR)CoreSig.fst $(CDIR)CoreDH.fst $(CDIR)DER.fst

TDIR=$(MITLS)ML/MiTLS-Modified/
TLSI=$(TDIR)TLSError.fsi $(TDIR)Nonce.fsi $(TDIR)TLSConstants.fsi $(TDIR)RSAKey.fsi $(TDIR)DHGroup.fsi $(TDIR)PMS.fsi $(TDIR)HASH.fsi #$(TDIR)HMAC.fsi $(TDIR)Sig.fsi $(TDIR)Cert.fsi $(TDIR)TLSInfo.fsi $(TDIR)TLSExtensions.fsi $(TDIR)TLSPRF.fsi $(TDIR)Range.fsi $(TDIR)DataStream.fsi $(TDIR)AppFragment.fsi $(TDIR)HSFragment.fsi $(TDIR)TLSFragment.fsi $(TDIR)StatefulPlain.fsi $(TDIR)LHAEPlain.fsi $(TDIR)MAC_SHA256.fsi $(TDIR)MAC_SHA1.fsi $(TDIR)MAC.fsi $(TDIR)Encode.fsi $(TDIR)ENC.fsi $(TDIR)AEAD_GCM.fsi $(TDIR)LHAE.fsi $(TDIR)StatefulLHAE.fsi $(TDIR)Record.fsi $(TDIR)Alert.fsi $(TDIR)PRF.fsi $(TDIR)KEF.fsi $(TDIR)DH.fsi $(TDIR)RSA.fsi $(TDIR)SessionDB.fsi $(TDIR)Handshake.fsi $(TDIR)AppData.fsi $(TDIR)Dispatch.fsi $(TDIR)TLS.fsi 

TLS=$(TDIR)TLSError.fsi $(TDIR)TLSError.fs $(TDIR)Nonce.fs $(TDIR)TLSConstants.fs $(TDIR)RSAKey.fs $(TDIR)DHGroup.fs $(TDIR)PMS.fs $(TDIR)HASH.fs $(TDIR)HMAC.fs $(TDIR)Sig.fsi $(TDIR)Cert.fst $(TDIR)TLSInfo.fs $(TDIR)TLSExtensions.fsi  $(TDIR)TLSPRF.fst $(TDIR)Range.fsi $(TDIR)Range.fs $(TDIR)DataStream.fsi $(TDIR)AppFragment.fsi $(TDIR)AppFragment.fs $(TDIR)HSFragment.fs $(TDIR)TLSFragment.fsi $(TDIR)TLSFragment.fs $(TDIR)StatefulPlain.fsi $(TDIR)StatefulPlain.fs $(TDIR)LHAEPlain.fsi $(TDIR)LHAEPlain.fs $(TDIR)MAC_SHA256.fs $(TDIR)MAC_SHA1.fs $(TDIR)MAC.fsi $(TDIR)MAC.fs $(TDIR)Encode.fsi $(TDIR)Encode.fs $(TDIR)ENC.fs #$(TDIR)AEAD_GCM.fs $(TDIR)LHAE.fs $(TDIR)StatefulLHAE.fs $(TDIR)Record.fs #$(TDIR)Alert.fs $(TDIR)PRF.fs $(TDIR)KEF.fs $(TDIR)DH.fs $(TDIR)RSA.fs $(TDIR)SessionDB.fst # $(TDIR)HandshakeMessages.fs $(TDIR)Handshake.fs $(TDIR)AppData.fs $(TDIR)Dispatch.fs $(TDIR)TLS.fs $(TDIR)TLS.fs

mitls:
	$(FSTAR) $(OTHERFLAGS) --debug yes --admit_fsi DataStream --admit_fsi Sig --pretype --codegen OCaml --prims prims.fst string.fst list.fst $(PLATFORM) $(CRYPTO) $(TLS)


wc: prims.fst $(ALL)
	wc -l $^

clean:
	rm *~ 
