In WSL, Conan 2.x stores everything in `~/.conan2/`. To clear cached packages:

```bash
# Nuke all cached packages, builds, downloads (keeps your profiles/config)
conan cache clean "*"
```

`conan cache clean` by default removes temporary build folders and downloads but keeps the final packages. To be more aggressive:

```bash
# Clean everything: sources, builds, downloads for all recipes
conan cache clean "*" --source --build --download --temp
```

**To remove the actual installed packages too** (full wipe of the cache):

```bash
conan remove "*" --confirm
```

That removes every recipe and binary from the cache. Your profiles in `~/.conan2/profiles/` and `global.conf` stay intact, so you don't have to re-run `conan profile detect`.

**Check what's there / how big first:**

```bash
du -sh ~/.conan2
conan list "*"          # see cached recipes
```

**Most thorough** (if you want to start completely fresh, including profiles):

```bash
rm -rf ~/.conan2
```

You'd then need `conan profile detect --force` again before next use.

---

Recommended order for your cleanup: run `conan remove "*" --confirm` first, then the vcpkg buildtrees cleanup, *then* the diskpart compact / sparse enable — so all the freed space gets reclaimed in one pass.

Good instinct to pause — Microsoft disabled sparse-by-default precisely because of corruption reports, so that warning isn't boilerplate. Here's the honest ranking from safest to riskiest:

**1. diskpart compact (safest, recommended)**

This is read-only by design — it attaches the VHDX as read-only, compacts, detaches. It cannot corrupt your filesystem because it never writes to the ext4 data, it just trims unused blocks at the container level. This is what you want.

```powershell
wsl --shutdown
# wait ~10 sec
diskpart
```
Then inside diskpart:
```
select vdisk file="C:\Users\62822\AppData\Local\wsl\{b8b91709-7745-4d3f-a34a-fde14b963c58}\ext4.vhdx"
attach vdisk readonly
compact vdisk
detach vdisk
exit
```

You saw diskpart open and immediately return to the prompt above — that's because you typed `diskpart` then it launched in a new interactive session. You need to type the `select vdisk...` lines *inside* the diskpart prompt (it changes to `DISKPART>`).

**2. Nuke and reinstall the distro (also very safe, more drastic)**

Zero corruption risk since you're creating a fresh VHDX. The cost is you rebuild your environment. Worth it if your WSL is already bloated with stuff you don't need.

```powershell
# OPTIONAL backup first — exports your whole distro to a tar
wsl --export Ubuntu-26.04 D:\ubuntu-backup.tar

# Remove the distro (deletes the VHDX entirely)
wsl --unregister Ubuntu-26.04

# Reinstall fresh
wsl --install -d Ubuntu-26.04
```

`--unregister` permanently deletes that distro's VHDX and everything in it, so only do it if you've backed up anything you care about (or your real work lives in `/mnt/c/...` on Windows, which is untouched). Your project at `/mnt/c/Users/62822/royyan/...` is on the Windows drive, so that's safe regardless.

**3. Sparse VHD with `--allow-unsafe` (riskiest — skip it)**

This is the one Microsoft gated behind a warning. Don't use it for a machine you do real work on.

---

**My recommendation for you:** go with diskpart compact. It's safe, reversible, and reclaims the current bloat without touching your data. Run the Conan/vcpkg cleanup inside WSL first, `wsl --shutdown`, then the diskpart sequence with the prompts entered *inside* the `DISKPART>` session.

If your WSL has accumulated a lot of junk over time and you'd rather start clean, option 2 is the nuclear-but-safe choice — just export first.
