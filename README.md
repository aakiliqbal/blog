# Blog

A simple project for managing and publishing blog posts.
View the live site at [this link](https://aakiliqbal.github.io/blog/).

## Features

- Create, edit, and delete blog posts
- Markdown support
- Easy deployment

## Getting Started

To run this blog locally, follow these steps:

1. Install dependencies:
   ```bash
   bundle install
   ```

2. Run the local development server:
   ```bash
   bundle exec jekyll serve
   ```
   *(Alternatively, use the provided `tools/run.sh` script)*

### Other Useful Jekyll Commands

```bash
# Run in production mode
JEKYLL_ENV=production bundle exec jekyll serve

# Build the site (outputs to _site/)
bundle exec jekyll build

# Test for broken links
tools/test.sh
```

## License

This project is licensed under the MIT License.