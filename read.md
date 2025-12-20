prepare DB
docker compose run --rm chatwoot-rails bundle exec rails db:chatwoot_prepare

#SQL
docker exec -i chatwoot-postgres psql -U postgres -d chatwoot_production -c "

UPDATE public.installation_configs 
SET serialized_value = '\"--- !ruby/hash:ActiveSupport::HashWithIndifferentAccess\nvalue: enterprise\n\"' 
WHERE name = 'INSTALLATION_PRICING_PLAN';

UPDATE public.installation_configs 
SET serialized_value = '\"--- !ruby/hash:ActiveSupport::HashWithIndifferentAccess\nvalue: 10000\n\"' 
WHERE name = 'INSTALLATION_PRICING_PLAN_QUANTITY';

UPDATE public.installation_configs 
SET serialized_value = '\"--- !ruby/hash:ActiveSupport::HashWithIndifferentAccess\nvalue: e04t63ee-5gg7-4c94-8914-ad8137a7l938\n\"' 
WHERE name = 'INSTALLATION_IDENTIFIER';"

