.PHONY: validate reload fmt

fmt:
	docker exec caddy caddy fmt --overwrite /config/Caddyfile

validate:
	docker exec caddy caddy validate --config /config/Caddyfile

reload:
	docker exec caddy caddy reload --config /config/Caddyfile

