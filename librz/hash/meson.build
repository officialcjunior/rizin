rz_hash_sources = [
  'msg_digest.c',
  'p/algo_crca.c',
  'p/algo_adler32.c',
  'p/algo_fletcher.c',
  'p/algo_md4.c',
  'p/algo_md5.c',
  'p/algo_mod255.c',
  'p/algo_sha1.c',
  'p/algo_sha256.c',
  'p/algo_sha384.c',
  'p/algo_sha512.c',
  'p/algo_xor8.c',
  'p/algo_xor16.c',
  'p/algo_xxhash32.c',
  'p/algo_parity.c',
  'p/algo_entropy.c',
  'p/algo_entropy_fractional.c',
  'algorithms/mod255/mod255.c',
  'algorithms/parity/parity.c',
  'algorithms/entropy/entropy.c',
  'algorithms/adler32/adler32.c',
  'algorithms/crc/crca.c',
  'algorithms/xor/xor.c',
  'algorithms/fletcher/fletcher.c'
]

dependencies = [mth, rz_util_dep, xxhash_dep]

if sys_openssl.found()
  dependencies += [sys_openssl]
else
  rz_hash_sources += [
    'algorithms/md4/md4.c',
    'algorithms/md5/md5.c',
    'algorithms/sha1/sha1.c',
    'algorithms/sha2/sha2.c'
  ]
endif

rz_hash = library('rz_hash', rz_hash_sources,
  include_directories: [platform_inc],
  c_args: library_cflags,
  dependencies: dependencies,
  install: true,
  implicit_include_directories: false,
  install_rpath: rpath_lib,
  soversion: rizin_libversion
)

rz_hash_dep = declare_dependency(link_with: rz_hash,
                                include_directories: [platform_inc])

pkgconfig_mod.generate(rz_hash,
  subdirs: 'librz',
  version: rizin_version,
  name: 'rz_hash',
  filebase: 'rz_hash',
  libraries: pkgcfg_sanitize_libs,
  requires: [
    'rz_util'
  ],
  description: 'rizin foundation libraries'
)
