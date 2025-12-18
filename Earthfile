VERSION 0.8

bundle:
	FROM docker.io/library/ruby:3.3
	COPY --dir Gemfile Gemfile.lock \
		/src/site
	WORKDIR /src/site
	RUN bundle install

nanoc:
	#FROM docker.io/library/ruby:3.3-alpine
	FROM +bundle
	COPY --dir content layouts lib Gemfile Gemfile.lock Rules nanoc.yaml \
		/src/site/


build:
	FROM +nanoc
    ARG base_url=infrastructure.openrobotics.org
	RUN INFRA_BASE_URL=$base_url bundle exec nanoc
	SAVE ARTIFACT output AS LOCAL output


bundle-update:
	FROM +nanoc
	RUN bundle update
	SAVE ARTIFACT Gemfile.lock AS LOCAL Gemfile.lock
