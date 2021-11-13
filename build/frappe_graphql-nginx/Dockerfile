FROM bitnami/node:12-prod

COPY build/frappe_graphql-nginx/install_app.sh /install_app

RUN chmod +x /install_app && /install_app frappe_graphql https://github.com/leam-tech/frappe_graphql

FROM frappe/erpnext-nginx:v13.14.1

COPY --from=0 /home/frappe/frappe-bench/sites/ /var/www/html/
COPY --from=0 /rsync /rsync
RUN echo -n "\nfrappe_graphql" >> /var/www/html/apps.txt

VOLUME [ "/assets" ]

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]