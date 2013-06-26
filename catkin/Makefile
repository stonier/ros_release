SHELL := /bin/bash

help:
	@echo "Valid git targets:"
	@echo "  clone  : clone all source and release repos."
	@echo "  pull   : pull latest from all source and release repos."
	@echo "  push   : push all release repos."
	@echo "  reset  : reset all release repos to HEAD state."
	@echo "  clean  : clear all cloned repos."
	@echo ""
	@echo "Valid bloom targets:"
	@echo "  config : point the release repo at the source repo (one time only)"
	@echo "  bloom  : run a release for the repo."

clone:
	@for i in ${REPOS}; do \
          git clone ${SRC_GIT}/$${i}.git; \
          git clone ${REL_GIT}/$${i}-release.git; \
        done

pull:
	@for i in ${REPOS}; do \
          cd ${CURDIR}/$${i}; git pull; \
          cd ${CURDIR}/$${i}-release; git pull; \
        done

push:
	@for i in ${REPOS}; do \
          cd ${CURDIR}/$${i}-release; git push --all; git push --tag; \
	done

reset:
	@for i in ${REPOS}; do \
          cd ${CURDIR}/$${i}-release; git reset --hard HEAD; \
	done

config:
	@for i in ${REPOS}; do \
          cd ${CURDIR}/$${i}-release; git-bloom-config new ${TRACK}; git push --all; git push --tag; \
	done

bloom:
	@for i in ${REPOS}; do \
          bloom-release --track ${TRACK} --rosdistro ${TRACK} $${i}; \
	done

clean:
	@for i in ${REPOS}; do \
          rm -rf $${i}; \
          rm -rf $${i}-release; \
        done
