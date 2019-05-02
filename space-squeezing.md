# Space Saving

Disk Usage Analyzer is helpful for visualizing disk usage.

## Articles

- <https://itsfoss.com/free-up-space-ubuntu-linux/>

### Key Points

- `sudo apt autoremove`
- `sudo du -sh /var/cache/apt`
  - `sudo apt autoclean`
  - `sudo apt clean`
- `du -sh ~/.cache/thumbnails`
  - `rm -rf ~/.cache/thumbnails/*`
- `sudo dpkg --list 'linux-image*'`
  - `sudo apt remove linux-image-VERSION`
- `sudo apt install gtkorphan`
  - Be careful and gentle with this method.
- Remove unused packages
  - shel: `sudo apt remove package-name package-name2`
- Remove duplicates use `FSLint` or `FDUPES`

## Languages

1. Open settings
2. Region & Language
3. Manage Installed Languages
4. Apply, Save, Profit