# Blog

A simple project for managing and publishing blog posts.
View the live site at [this link](https://aakiliqbal.github.io/blog/).

## Features

- Create, edit, and delete blog posts
- Markdown support
- Easy deployment

## Getting Started

To run this blog locally, install Ruby and the native build tools for your operating system first.

### Linux Prerequisites

Fedora:

```bash
sudo dnf install ruby ruby-devel gcc gcc-c++ make redhat-rpm-config
```

Ubuntu/Debian:

```bash
sudo apt update
sudo apt install ruby-full ruby-dev build-essential zlib1g-dev
```

Arch Linux:

```bash
sudo pacman -S ruby base-devel
```

### Windows Prerequisites

1. Install Ruby+Devkit from [RubyInstaller](https://rubyinstaller.org/downloads/).
2. Open the **Start Command Prompt with Ruby** shortcut.
3. Install the MSYS2 build toolchain when prompted, or run:

```powershell
ridk install
```

### Run Locally

1. Install dependencies:

   ```bash
   bundle install
   ```

2. Run the local development server:

   ```bash
   bundle exec jekyll serve
   ```

3. Open the local site:

   ```text
   http://127.0.0.1:4000/blog/
   ```

On Linux/macOS, you can also use the provided helper script:

```bash
tools/run.sh
```

### Other Useful Jekyll Commands

```bash
# Run in production mode
JEKYLL_ENV=production bundle exec jekyll serve

# Build the site (outputs to _site/)
bundle exec jekyll build

# Test for broken links
tools/test.sh
```

On Windows, use the equivalent Bundler commands directly:

```powershell
bundle exec jekyll serve
bundle exec jekyll build
bundle exec htmlproofer ./_site
```

## License

This project is licensed under the MIT License.
