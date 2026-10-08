# browser-image-compression 2.0.2: small PNG still converted in Chromium

[Download the full reproduction ZIP](browser-image-compression-2.0.2-repro.zip) (36772 bytes). SHA-256: 6a95a56a8557abb1c8d74bb7c1fba92197d52c4535b019f8a92e0c1d6ddb48fe.


This is a bounded, independent reproduction for
[issue #241](https://github.com/Donaldcwl/browser-image-compression/issues/241). It does not test
the original reporter's file, React/Vite integration, Safari/iOS or Android.

On 8 October 2026, Chromium 155 with a Windows user-agent converted the supplied synthetic
82,643-byte PNG to an 11,160-byte WebP using the exact reported options. Dimensions remained
6000×4000. The real worker returned one file result without an error; main-thread control returned
identical bytes. Both were independently decoded with Pillow as WebP. Input below maxSizeMB
therefore did not, by itself, skip the requested conversion in this case.

## Run the same case

1. Extract the complete ZIP to a new local folder. Keep its package subdirectory intact.
2. Run node server.mjs from that folder (tested with Node.js 24). It prints a 127.0.0.1 URL and
   chooses an available port. It serves only the fixed harness assets and accepts only its three
   result files, same origin, up to 2 MiB each.
3. Open that URL in a Chromium browser. Select the provided fixture.png using the file picker. Use
   only this synthetic fixture; this harness is not a general private-image upload service.
4. Click Run reproduction. The page shows exact input/output MIME, bytes, SHA256, dimensions, object
   identity, worker completion/error counters and browser user-agent.
5. The local server saves results.json, worker-output.bin and main-output.bin in this folder. The
   shipped copies are the actual recorded results, not expectations. Close the server with Ctrl+C
   when done. All script/worker URLs and result writes stay on localhost.

Options: maxSizeMB 0.156, fileType image/webp, useWebWorker true, alwaysKeepResolution true,
maxIteration 50, plus a same-origin libURL pinned to the bundled 2.0.2 script. The control changes
only useWebWorker to false. A direct canvas WebP capability probe is also recorded.

The original is a fully synthetic grid, not a customer photo. Source SHA256:
0e98a4cf34fc49519a6d5f8a362ed3c5f87fba33c9a5e9e16c4b0772ed38f014. Both output SHA256:
9c745420586f056ebedadd6b11052273e080c67c208868ba501aa6c4bda69802. The Safari token in the Chromium
user-agent is not Safari test coverage.

## Published package and source

Official npm version: https://registry.npmjs.org/browser-image-compression/2.0.2

Bundled UMD SHA256: c6713a21756570af4c230f706faac4f0187845928bd14fd5910210d1cdc6fb87. Its original
MIT license and Donald Chan copyright are retained in package/LICENSE. That third-party license
describes the bundled library, not Refentra's application source. The original npm tarball was
verified against registry SHA512 integrity before extraction.

The npm source map matched the tagged source exactly.
[Immutable source, lines 73–94](https://github.com/Donaldcwl/browser-image-compression/blob/d933bc8e483a9853ed2b57338e035e8c45e40dc7/lib/image-compression.js#L73-L94)
encodes a tempFile with outputFileType before the size checks; its early exit returns that encoded
tempFile. This is consistent with this successful result and is not a diagnosis of every failure.

Prepared by Refentra's operator with AI-assisted analysis and browser testing. No product link,
universal compatibility claim, quality guarantee, endorsement or adoption is implied.
