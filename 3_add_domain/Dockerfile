FROM workingman/wls:1221dev

ARG ADMIN_PASSWORD
ARG ADMIN_NAME
ARG DOMAIN_NAME
ARG ADMIN_PORT
ARG CLUSTER_NAME
ARG DEBUG_FLAG
ARG PRODUCTION_MODE

ENV ADMIN_HOST="wlsadmin" \
    NM_PORT="5556" \
    MS_PORT="7002" \
    DEBUG_PORT="8453" \
    CONFIG_JVM_ARGS="-Dweblogic.security.SSL.ignoreHostnameVerification=true"

ENV DOMAIN_NAME="${DOMAIN_NAME:-base_domain}" \
    DOMAIN_HOME=/u01/oracle/user_projects/domains/${DOMAIN_NAME:-base_domain} \
    ADMIN_PASSWORD="${ADMIN_PASSWORD:-welcome1}" \
    ADMIN_NAME="${ADMIN_NAME:-AdminServer}" \
    ADMIN_PORT="${ADMIN_PORT:-7001}" \
    CLUSTER_NAME="${CLUSTER_NAME:-DockerCluster}" \
    debugFlag="${DEBUG_FLAG:-false}" \
    PRODUCTION_MODE="${PRODUCTION_MODE:-prod}" \
    PATH=$PATH:/u01/oracle/oracle_common/common/bin:/u01/oracle/wlserver/common/bin:/u01/oracle/user_projects/domains/${DOMAIN_NAME:-base_domain}/bin:/u01/oracle

USER oracle
COPY container-scripts/* /u01/oracle/

RUN /u01/oracle/wlst /u01/oracle/create-wls-domain.py && \
    mkdir -p /u01/oracle/user_projects/domains/$DOMAIN_NAME/servers/AdminServer/security && \
    echo "username=weblogic" > /u01/oracle/user_projects/domains/$DOMAIN_NAME/servers/AdminServer/security/boot.properties && \
    echo "password=$ADMIN_PASSWORD" >> /u01/oracle/user_projects/domains/$DOMAIN_NAME/servers/AdminServer/security/boot.properties && \
    echo ". /u01/oracle/user_projects/domains/$DOMAIN_NAME/bin/setDomainEnv.sh" >> /u01/oracle/.bashrc 

# Expose Node Manager default port, and also default for admin and managed server 
EXPOSE $NM_PORT $ADMIN_PORT $MS_PORT $DEBUG_PORT

WORKDIR $DOMAIN_HOME

# Define default command to start bash. 
CMD ["startWebLogic.sh"]
