FROM ruby:2.7.1-alpine

RUN	mkdir -p /aws && \
	apk -Uuv add groff less python py-pip git openssh && \
	pip install awscli && \
	apk --purge -v del py-pip && \
	rm /var/cache/apk/*

RUN apk add --update ruby-dev build-base libffi-dev
RUN apk add --update tar # for circle ci cache
RUN apk add --update openjdk7-jre
