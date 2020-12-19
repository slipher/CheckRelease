Script that checks an Unvanquished release for various possible mistakes.

Usage:

    check_release.py <release zip file> <version number>
    
The script has been tested on Linux and Windows. `readelf` even works on Windows if you have MinGW installed: for some reason, they ship a readelf which works on (only) Linux binaries.

Checks performed:
- Linux binaries are built as position-independent executables (for security)
- All Breakpad symbol files exist and have some of the expected content
- Hashes in `pkg/md5sums` match the packages

Running the script on the 0.51 release produces the following output:

    # python3 check_release.py unvanquished_0.51.1.zip 0.51.1
    Linux binary 'daemon' appears not to be PIE
    Linux binary 'daemonded' appears not to be PIE
    Linux binary 'daemon-tty' appears not to be PIE
    Symbol file 'symbols/daemon-tty/943FEC32CDACF42E86E04FD87004F21E0/daemon-tty.sym' doesn't appear to actually have symbols (mistakenly used stripped binary?)
    Symbol file 'symbols/daemon/F8A1F45833C1977CD13657473592668C0/daemon.sym' doesn't appear to actually have symbols (mistakenly used stripped binary?)
    Symbol file 'symbols/daemonded/8B93DD8B64AA4CB9D7590EBCBD6CACA50/daemonded.sym' doesn't appear to actually have symbols (mistakenly used stripped binary?)
    Missing md5sums file in pkg/
