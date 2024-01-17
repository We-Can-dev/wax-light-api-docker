init-light_api: ## Initialize light API indexer no start
	@echo "!!!WARNING: Irreversible actions!!!"
	@echo ""
	@while [ -z "$$CONTINUE" ]; do \
			read -r -p "Do you really want to proceed? [y/N]: " CONTINUE; \
	done ; \
	( [ $$CONTINUE = "y" ] || [ $$CONTINUE = "Y" ] ) && ansible-playbook --diff init-light_api.yml --tags deploy_config,init_light_api_api || (echo "Deploy cancelled.";)

init-backups_light_api: ## Initialize light API BACKUP
	@echo "!!!WARNING: Irreversible actions!!!"
	@echo ""
	@while [ -z "$$CONTINUE" ]; do \
			read -r -p "Do you really want to proceed? [y/N]: " CONTINUE; \
	done ; \
	( [ $$CONTINUE = "y" ] || [ $$CONTINUE = "Y" ] ) && ansible-playbook --diff init-light_api.yml --tags backup_light_api || (echo "Deploy cancelled.";)

startup-cluster_light_api: ## Initialize light API indexer no start
	@echo "!!!WARNING: Irreversible actions!!!"
	@echo ""
	@while [ -z "$$CONTINUE" ]; do \
			read -r -p "Do you really want to proceed? [y/N]: " CONTINUE; \
	done ; \
	( [ $$CONTINUE = "y" ] || [ $$CONTINUE = "Y" ] ) && ansible-playbook --diff init-light_api.yml --tags deploy_config,init_light_api_api,startup_light_api || (echo "Deploy cancelled.";)

deploy-light_api_configs: ## Deploy light config changes
	@echo "!!!WARNING: Irreversible actions!!!"
	@echo ""
	@while [ -z "$$CONTINUE" ]; do \
			read -r -p "Do you really want to proceed? [y/N]: " CONTINUE; \
	done ; \
	( [ $$CONTINUE = "y" ] || [ $$CONTINUE = "Y" ] ) && ansible-playbook --diff init-light_api.yml --tags deploy_config || (echo "Deploy cancelled.";)

nuke-light_data: stop-cluster_light ## Destroy light-api data
	@echo "!!!WARNING: Irreversible actions!!!"
	@echo ""
	@while [ -z "$$CONTINUE" ]; do \
			read -r -p "Do you really want to proceed? [y/N]: " CONTINUE; \
	done ; \
	( [ $$CONTINUE = "y" ] || [ $$CONTINUE = "Y" ] ) && 	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'rm -rf /opt/wax/light_api/${ENV}/{chronicle,mariadb,config};'  || exit 0

restore-lightapi_db_dump: ## RESTORE WAX Lightapi db snapshots
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) '/usr/bin/screen -dmS lightapi_restore bash /opt/wax/light_api/${ENV}/mariadb/snapshots/restore_db.sh'

restore-chronicle_snapshot: ## RESTORE WAX Lightapi Chronicle snapshots
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) '/usr/bin/screen -dmS chronicle_restore bash /opt/wax/light_api/${ENV}/config/chronicle_snapshot_restore.sh'

restore-chronicle_speed_up_restore: ## RESTORE WAX Lightapi Chronicle - restart with 10 sec timeout to speed up sync
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) '/usr/bin/screen -dmS chronicle_speed_restore bash /opt/wax/light_api/${ENV}/config/chronicle_speed_restore.sh.sh'

start-container_chronicle: ## Start light indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose up -d eosio-lightapi-chronicle'  || exit 0

stop-container_chronicle: ## Stop light indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose rm -f -s -v eosio-lightapi-chronicle'  || exit 0

restart-container_chronicle: stop-container_chronicle start-container_chronicle

start-container_dbwriter: ## Start light indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose up -d eosio-lightapi-dbwriter'  || exit 0

stop-container_dbwriter: ## Stop light indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose rm -f -s -v eosio-lightapi-dbwriter'  || exit 0

restart-container_dbwriter: stop-container_dbwriter start-container_dbwriter

start-container_wsapi: ## Start light indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose up -d eosio-lightapi-wsapi'  || exit 0

stop-container_wsapi: ## Stop light indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose rm -f -s -v eosio-lightapi-wsapi'  || exit 0

restart-container_wsapi: stop-container_wsapi start-container_wsapi

start-container_light_api: ## Start light indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose up -d eosio-lightapi'  || exit 0

stop-container_light_api: ## Stop light indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose rm -f -s -v eosio-lightapi'  || exit 0

restart-container_light_api: stop-container_light_api start-container_light_api

start-container_light_api_cron: ## Start light API
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose up -d eosio-lightapi-cron'  || exit 0

stop-container_light_api_cron: ## Stop light API
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose rm -f -s -v eosio-lightapi-cron'  || exit 0

restart-container_light_api_cron: stop-container_light_api_cron start-container_light_api_cron

start-container_mariadb: ## Start light API
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose up -d eosio-lightapi-mariadb'  || exit 0

stop-container_mariadb: ## Stop light API
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'cd /opt/wax/light_api/${ENV}; docker-compose rm -f -s -v eosio-lightapi-mariadb'  || exit 0

restart-container_mariadb: stop-container_mariadb start-container_mariadb

stop-cluster_light_api: ## Stop All light components
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'su - wax -c "cd /opt/wax/light_api/${ENV}; docker-compose down"'  || exit 0

log-chronicle: ## Tail logs from light API
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'docker logs -n 50 -f eosio-lightapi-chronicle' || exit 0

log-dbwriter: ## Tail logs from light Indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'docker logs -n 50 -f eosio-lightapi-dbwriter' || exit 0

log-wsapi: ## Tail logs from light Indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'docker logs -n 50 -f eosio-lightapi-wsapi' || exit 0

log-light_api: ## Tail logs from light Indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'docker logs -n 50 -f eosio-lightapi' || exit 0

log-light_api_cron: ## Tail logs from light Indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'docker logs -n 50 -f eosio-lightapi-cron' || exit 0

log-mariadb: ## Tail logs from light Indexer
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'docker logs -n 50 -f eosio-lightapi-mariadb' || exit 0

log-light_api_sync: ## Check Light APi sync
	ssh -o StrictHostKeyChecking=no root@$(TARGET_HOST) 'bash /opt/wax/light_api/${ENV}/config/chronicle_sync_check.sh'