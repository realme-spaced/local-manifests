# LineageOS build manifest for Realme 8i / Narzo 50 (spaced)

## Build Steps

### Setup environment
 - Fetch repo and make it executable
```sh
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```
 - Include repo into your path

Add these lines inside you ~/.bashrc or ~/.zshrc
```sh
if [ -d "$HOME/bin" ] ; then
PATH="$HOME/bin:$PATH"
fi
```

- Configure git 
```sh
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
git lfs install
```

- Setup directory for lineage
```sh
mkdir -p lineage/20.0
```

### Fetch

- Fetch lineage

```sh
cd lineage/20.0
repo init -u https://github.com/LineageOS/android.git -b lineage-20.0 --git-lfs
repo sync
```
- Fetch device

```sh
git clone https://github.com/realme-spaced/local_manifests .repo/local_manifests
repo sync
```

- Extract proprietary blobs

 Move into device directory

```sh
cd device/realme/spaced
```

Extract proprietary blobs either directly from an extracted firmware,

```sh
./extract-files.sh </path/to/extracted/firmware>
./extract-files-ims.sh </path/to/extracted/firmware>
```

or from your phone connected to your computer via the USB cable, with ADB and root enabled.

```sh
./extract-files.sh
./extract-files-ims.sh
```

Return back to lineage directory
```sh
cd ../../../
```

### Build

```sh
. build/envsetup.sh
lunch lineage_spaced-eng
brunch spaced
```