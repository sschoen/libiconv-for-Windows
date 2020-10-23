CMAKE_MINIMUM_REQUIRED  (VERSION 3.12)
PROJECT                 (LibIconv)

# options
OPTION                  (ICONV_BUILD_SHARED_LIBS "Build shared libraries" ON)
OPTION                  (ICONV_BUILD_STATIC_LIBS "Build static libraries" ON)
OPTION                  (ICONV_SET_OUTPUT_DIRECTORIES "Set output directories" ON)

# needed packages
SET                     (CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake_modules")

# includes and outputs
SET                     (CMAKE_INCLUDE_CURRENT_DIR on)
SET                     (INCLUDE_DIR "${PROJECT_SOURCE_DIR}/include")
INCLUDE_DIRECTORIES     (BEFORE SYSTEM
                          ${INCLUDE_DIR}
                          "${PROJECT_SOURCE_DIR}/libiconv-1.16/libcharset/include"
                          "${PROJECT_SOURCE_DIR}/libiconv-1.16/include"
                          "${PROJECT_SOURCE_DIR}/libiconv-1.16"
                        )
IF                      (ICONV_SET_OUTPUT_DIRECTORIES)
  SET                     (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/plugin)
  SET                     (CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
ENDIF                   ()

# compiler settings
SET                     (CMAKE_CXX_STANDARD 17)
SET                     (CMAKE_CXX_STANDARD_REQUIRED on)
# Linux
#IF                      (${CMAKE_SYSTEM_NAME} STREQUAL "Linux")
#  MESSAGE                 ("Unix-like system: ${CMAKE_SYSTEM_NAME}")
# Windows
ELSEIF                  (${CMAKE_SYSTEM_NAME} STREQUAL "Windows")
  MESSAGE                 ("Windows-like system: ${CMAKE_SYSTEM_NAME}")
# Unsupported
ELSE                    ()
  MESSAGE                 (FATAL_ERROR "unsupported system: ${CMAKE_SYSTEM_NAME}")
ENDIF                   ()

# source code stuff starts here

SET                     (tmpFiles 
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases.gperf
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_sysaix.gperf
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_syshpux.gperf
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_sysosf1.gperf
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_syssolaris.gperf
                          #${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/encodings.def
                          #${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/encodings_aix.def
                          #${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/encodings_dos.def
                          #${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/encodings_extra.def
                          #${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/encodings_local.def
                          #${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/encodings_osf1.def
                          #${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/translit.def
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iconv.c
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/relocatable.c

                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/libcharset/lib/localcharset.c
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/libcharset/lib/relocatable-stub.c

                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/libcharset/include/libcharset.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/libcharset/include/localcharset.h

                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/include/iconv.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases2.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_aix.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_aix_sysaix.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_dos.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_extra.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_osf1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_osf1_sysosf1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_sysaix.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_syshpux.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_sysosf1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/aliases_syssolaris.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/armscii_8.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ascii.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/atarist.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/big5.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/big5hkscs1999.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/big5hkscs2001.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/big5hkscs2004.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/big5hkscs2008.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/big5_2003.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/c99.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_aix.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_aix_sysaix.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_dos.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_extra.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_local.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_local_sysaix.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_local_syshpux.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_local_sysosf1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_local_syssolaris.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_osf1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_osf1_sysosf1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_sysaix.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_syshpux.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_sysosf1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/canonical_syssolaris.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ces_big5.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ces_gbk.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cjk_variants.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_15.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_2.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_3.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_4.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_4a.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_4b.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_5.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_6.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_7.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cns11643_inv.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/config.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/converters.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1046.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1124.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1125.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1129.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1131.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1133.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1161.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1162.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1163.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1250.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1251.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1252.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1253.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1254.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1255.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1256.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1257.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp1258.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp437.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp50221_0208_ext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp50221_0212_ext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp737.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp775.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp850.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp852.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp853.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp855.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp856.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp857.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp858.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp860.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp861.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp862.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp863.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp864.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp865.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp866.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp869.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp874.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp922.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp932.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp932ext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp936.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp936ext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp943.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp949.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp950.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/cp950ext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/dec_hanyu.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/dec_kanji.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/euc_cn.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/euc_jisx0213.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/euc_jp.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/euc_kr.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/euc_tw.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/flags.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/flushwc.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gb12345.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gb12345ext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gb18030.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gb18030ext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gb18030uni.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gb2312.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gbk.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gbkext1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gbkext2.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/gbkext_inv.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/georgian_academy.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/georgian_ps.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/hkscs1999.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/hkscs2001.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/hkscs2004.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/hkscs2008.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/hp_roman8.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/hz.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iconv_open1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iconv_open2.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso2022_cn.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso2022_cnext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso2022_jp.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso2022_jp1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso2022_jp2.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso2022_jp3.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso2022_jpms.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso2022_kr.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso646_cn.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso646_jp.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_10.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_11.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_13.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_14.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_15.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_16.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_2.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_3.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_4.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_5.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_6.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_7.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_8.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/iso8859_9.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/isoir165.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/isoir165ext.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/java.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/jisx0201.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/jisx0208.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/jisx0212.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/jisx0213.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/johab.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/johab_hangul.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/koi8_r.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/koi8_ru.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/koi8_t.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/koi8_u.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ksc5601.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/loops.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/loop_unicode.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/loop_wchar.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_arabic.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_centraleurope.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_croatian.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_cyrillic.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_greek.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_hebrew.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_iceland.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_roman.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_romania.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_thai.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_turkish.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mac_ukraine.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/mulelao.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/nextstep.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/pt154.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/relocatable.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/riscos1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/rk1048.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/shift_jisx0213.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/sjis.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/tcvn.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/tds565.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/tis620.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/translit.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs2.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs2be.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs2internal.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs2le.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs2swapped.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs4.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs4be.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs4internal.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs4le.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/ucs4swapped.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/uhc_1.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/uhc_2.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/utf16.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/utf16be.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/utf16le.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/utf32.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/utf32be.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/utf32le.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/utf7.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/utf8.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/vietcomb.h
                          ${PROJECT_SOURCE_DIR}/libiconv-1.16/lib/viscii.h

                          ${PROJECT_SOURCE_DIR}/include/iconv.h
                          ${PROJECT_SOURCE_DIR}/res/libiconv.rc

                          ${PROJECT_SOURCE_DIR}/LICENSE
                          ${PROJECT_SOURCE_DIR}/README.md
                        )
SOURCE_GROUP            (TREE ${PROJECT_SOURCE_DIR} FILES ${tmpFiles})

SET                     (TPL_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG}")
SET                     (TPL_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE}")

IF                      (CMAKE_CONFIGURATION_TYPES)
  SET                     (CMAKE_CONFIGURATION_TYPES Debug Release)
  SET                     (CMAKE_CONFIGURATION_TYPES "${CMAKE_CONFIGURATION_TYPES}" CACHE STRING "Reset the configurations to what we need" FORCE)
ENDIF                   ()

IF                      (ICONV_BUILD_STATIC_LIBS)
  SET                     (CMAKE_CXX_FLAGS_DEBUG "${TPL_FLAGS_DEBUG} -D_LIB -DUSING_STATIC_LIBICONV")
  SET                     (CMAKE_CXX_FLAGS_RELEASE "${TPL_FLAGS_RELEASE} -D_LIB -DUSING_STATIC_LIBICONV")

  ADD_LIBRARY             ("libiconvStatic" STATIC ${tmpFiles})
  SET_TARGET_PROPERTIES	  ("libiconvStatic" PROPERTIES LINKER_LANGUAGE CXX)
ENDIF                   ()
IF                      (ICONV_BUILD_SHARED_LIBS)
  SET                     (CMAKE_CXX_FLAGS_DEBUG "${TPL_FLAGS_DEBUG} -D_USRDLL -DBUILDING_LIBICONV -DBUILDING_LIBCHARSET -DLIBICONV_EXPORTS")
  SET                     (CMAKE_CXX_FLAGS_RELEASE "${TPL_FLAGS_RELEASE} -D_USRDLL -DBUILDING_LIBICONV -DBUILDING_LIBCHARSET -DLIBICONV_EXPORTS")

  ADD_LIBRARY             ("libiconv" MODULE ${tmpFiles})
  SET_TARGET_PROPERTIES   ("libiconv" PROPERTIES LINKER_LANGUAGE CXX)
ENDIF                   ()