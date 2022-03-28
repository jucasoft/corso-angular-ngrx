# nrwl-nx
https://github.com/marketplace/actions/nrwl-nx

# Google App Engine
https://github.com/google-github-actions/deploy-appengine

# nx-deploy-gae
progetto interessante per capire come cunfigurare i file yaml
https://github.com/beeman/nx-deploy-gae
seguito le istruzioni:
https://github.com/jucasoft/deploy-appengine#example-workflows


project-id test-deploy-1111
test-deploy-1111.appspot.com

my-service-account@test-deploy-1111.iam.gserviceaccount.com

# punto 5, creazione del servizio
gcloud iam service-accounts create my-service-account \
--description="my-service-account-desc" \
--display-name="my-service-account-name"

# add roles:
l'elenco dei ruoli da aggiungere non sono corretti, ho dovuto aggungerli da UI nella sezione iam

# creazione file service-account-keys
https://cloud.google.com/iam/docs/creating-managing-service-account-keys

gcloud iam service-accounts keys create sa-private-key.json \
--iam-account=my-service-account@test-deploy-1111.iam.gserviceaccount.com

# punto 8
GCP_PROJECT: test-deploy-1111
GCP_SA_KEY: il file json

git push https://github.com/jucasoft/deploy-appengine.git main:example
