# GeneMANIA pages

## Setup

- Make sure you have Ruby >=2.0.0 : `ruby --version`
- Make sure you have Rake : `which rake`
- Install Bundler and Jekyll : `gem install bundler jekyll`
- Install dependencies using Bundler : `bundle install`
- Update your dependencies regularly : `bundle update`

## Live preview

- Run Jekyll locally : `rake preview`
- Open [http://localhost:4000](http://localhost:4000) in your browser

## Publishing

- Whatever gets pushed to the `master` branch gets published
- Put incomplete posts in `_drafts`
- You can preview drafts with `rake drafts`
