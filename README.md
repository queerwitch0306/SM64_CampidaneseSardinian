# SM64 Campidanese Sardinian

Preservatzioni de sa Lingua Sarda imparis cun sa nostalgia e is videogiogus

Questa traduzione in Lingua Sarda Campidanese (nello specifico, Campidanese Occidentale) è realizzata per preservare il patrimonio culturale della lingua sarda, e sarà disponibile nonappena terminata in maniera accessibile e gratuita: verrà rilasciata sotto forma di un comodo patch BPS, che sarà applicabile alla rom tramite il sm64 rom patcher online.

La nostra patch è, e sarà sempre gratuita! Se hai pagato per riceverla, chiedi il rimborso!
Si accettano comunque mancie per il lavoro svolto, per maggiori informazioni contattare (contact info da mettere)

Essendo basato su UltraSM64, oltre a molte altre cose, supporta il rumble come la traduzione italiana di RulesLess!

Obbiettivi Principali:

-Tradurre interamente il testo del gioco in Sardo Campidanese;

-Localizzare le immagini che contengono testo

-Supporto per Emulatore, Nintendo 64, Wii VC, Wii U VC

-Dare più opzioni di patch, come per esempio permettere di usare la versione PAL per chi dispone di una Nintendo 64 o Wii PAL

Obbiettivi Estesi:

-Supporto PC Port

-Supporto SM64 Co-Op DX

-Supporto per Switch Online e 3D All-Stars

Translation by Jessu Group (founded by BrusciaMau/queerwitch0306)

# UltraSM64

- This repo contains a full decompilation of Super Mario 64 (J), (U), (E), and (SH).
- Naming and documentation of the source code and data structures are in progress.
- It has been edited to allow for the usage of the final "N64 OS" library, version ``2.0L``
- Shindou Rumble Pak code is on for all regions.
- Targeting the iQue Player is supported.
- Saving to 32kbyte/256kbit SRAM is supported.
- Newer compression options are supported.
- UNFLoader (flashcart USB library) is supported, allowing for debugging on EverDrive/64Drive.
- It has been patched with someone2639's shiftable segments patch
- Wiseguy's instant input patch has been added to allow for less input lag on emulation (Does not affect console)
  This does mean that any framebuffer effects will have to be done on buffer 0 if targeting emulators
- Automatic console and emulator detection: Use the `gIsConsole` variable to wrap your code in an emulator check.
- Separate defines for emulator and console black border height.
- Getting HVQM FMV support to work with the game is WIP.

Requirements are the same as regular SM64, however a GCC MIPS cross compiler is also required. If you're on Debian-like Linux, you can use the ``gcc-mips-linux-gnu`` package. The toolchain that comes with my SDK is also supported.

## Additional Prerequisites

BinPNG (the CI texture converter) requires some python3 dependencies. Use pip to install them.

``pip install pypng bitstring`` 

## UNFLoader support

The repository supports UNFLoader for debugging.

To build with UNF, run make with ``UNF=1``.

Further instructions can be found at the [official repository](https://github.com/buu342/N64-UNFLoader)

**NOTE: Closing the UNFLoader window will result in your game eventually hanging due to lacking a USB device to send messages to, so beware of that**

## Multi-Save support

The repository supports SRAM in addition to EEPROM. The standard save data functions are #ifdef'd to accommedate this.

To build with SRAM support, run make with ``SAVETYPE=sram``.

I may attempt FlashRAM in the future.

## Multi-Console support

The repository supports targeting the iQue Player in addition to the N64. The iQue libultra is ***NOT*** compatible with N64 in many ways, so it is currently NOT possible to have one build for both consoles.

To target iQue, run make with the ``CONSOLE=bb`` argument.

## Compression

The repo also supports RNC (Rob Northen Compression). RNC has two methods. 

Method 1 is designed to compress as small as possible, while method 2 is designed so that decompression is as fast as possible.

Method 1 is the current default, and is the best all-rounder in terms of speed and ratio.

Both methods are fast. Method 1 has better compression than 2, so I suggest using method 1 if using RNC.

To switch to RNC, run make with either ``COMPRESS=rnc1`` or ``COMPRESS=rnc2``, depending on preferred method.

The repository also supports using DEFLATE compression. This boasts a better compression ratio, but at a slight cost to load times.

On average I'd estimate that the bottleneck on decompression is about 1-2 seconds.

To switch to gzip, run make with the ``COMPRESS=gzip`` argument.

The repo also supports gziping with ``libdeflate-gzip``. This compresses at a slightly better ratio than standard ``gzip``, with no real downside from a decompression standpoint.

To use ``libdeflate-gzip``, first clone the [repo](https://github.com/ebiggers/libdeflate), then `make` and `make install` it.

Then run make for sm64 with ``GZIPVER=libdef`` in addition to ``COMPRESS=gzip``

The repo also supports building a ROM with no compression.

This is not recommended as it increases ROM size significantly, with little point other than load times decreased to almost nothing.

To switch to no compression, run make with the ``COMPRESS=uncomp`` argument.


## FAQ

Q: Why in the hell are you bundling your own build of ``ld``?

A: Newer binutils (Like the one bundled with Ubuntu, 2.34) break linking with libultra builds due to local asm symbols.

This puts me at a crossroads of either touching leaked code and requiring GCC, or just using an older linker that works just fine.

I went with the latter.

Thanks to "someone2639" for this hacky-ass idea

Q: Will this allow me to use FlashRAM/Transfer Pak/microcode swapping/Other Cool N64 Features?

A: Theoretically, all yes.

## Installation help

Go read the original repo README.md
