SHELL=/bin/zsh

.SECONDARY: 

.PHONY: 

all: 

clean:
	rm -rf office officeunpack preparestuff

domain_adaptation_images.tar.gz:
	@echo "*** can't automate google drive download :( ***" 1>&2
	@echo "https://drive.google.com/file/d/0B4IapRTv9pJ1WGZVd1VDMmhwdlE/view" 1>&2
	@exit 1

officeunpack: domain_adaptation_images.tar.gz
	test -d office || mkdir office
	(cd office && tar -zxf ../$<)
	(cd office && ln -sT . domain_adaptation_images)
	touch $@

preparestuff: officeunpack
	(cd ../.. && PYTHONPATH=./python ./examples/adaptation/scripts/prepare_experiments.sh ./examples/adaptation/office/)
	touch $@

model=amazon_to_webcam
train: ./experiments/$(model)/scripts/train.sh
	(cd ../.. && ./examples/adaptation/$<)
