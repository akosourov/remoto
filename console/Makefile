serve:
	dev_appserver.py dispatch.yaml www/app.yaml api/app.yaml

build: copyassets
	cd www ; npm run build # see build command in www/package.json

clean:
	rm -rf ./api/templates
	rm -rf ./www/vendor

copyassets: clean
	cp -R ../templates ./api/templates
	mkdir -p ./www/vendor/github.com/matryer/remoto
	cp -R ../remototypes ./www/vendor/github.com/matryer/remoto/remototypes/
	echo "Folder is generated by: make copyassets" >> ./www/vendor/README

deploy: build
	gcloud config set project remotoconsole
	gcloud app deploy www/app.yaml -v v1 -q
	gcloud app deploy api/app.yaml -v v1 -q
	gcloud app deploy dispatch.yaml -q
