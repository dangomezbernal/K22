# K22
configurar el /etc/krb5.conf --> establecer los realms en el server
```
[libdefaults]
        default_realm = EDT.ORG

# The following krb5.conf variables are only for MIT Kerberos.
        kdc_timesync = 1
        ccache_type = 4
        forwardable = true
        proxiable = true

# The following encryption type specification will be used by MIT Kerberos
# if uncommented.  In general, the defaults in the MIT Kerberos code are
# correct and overriding these specifications only serves to disable new
# encryption types as they are added, creating interoperability problems.
#
# The only time when you might need to uncomment these lines and change
# the enctypes is if you have local software that will break on ticket
# caches containing ticket encryption types it doesn't know about (such as
# old versions of Sun Java).

#       default_tgs_enctypes = des3-hmac-sha1
#       default_tkt_enctypes = des3-hmac-sha1
#       permitted_enctypes = des3-hmac-sha1

# The following libdefaults parameters are only for Heimdal Kerberos.
        fcc-mit-ticketflags = true

[realms]
  EDT.ORG = {
    kdc = kserver.edt.org
    admin_server = kserver.edt.org
  }

[domain_realm]
  .edt.org = EDT.ORG
  edt.org = EDT.ORG
```
configurar el kdc.conf --> cosas del servicio creo, en plan configuración y opciones como por ejemplo la vida util de los tickets y cosas asi (no existe el fichero, lo tienes que crear tu (creo que se generaba cuando iniciabas el servicio pero no estoy seguro))
```
[kdcdefaults]
    kdc_ports = 750,88

[realms]
    EDT.ORG = {
        database_name = /var/lib/krb5kdc/principal
        admin_keytab = FILE:/etc/krb5kdc/kadm5.keytab
        acl_file = /etc/krb5kdc/kadm5.acl
        key_stash_file = /etc/krb5kdc/stash
        kdc_ports = 750,88
        max_life = 10h 0m 0s
        max_renewable_life = 7d 0h 0m 0s
        master_key_type = des3-hmac-sha1
        #supported_enctypes = aes256-cts:normal aes128-cts:normal
        default_principal_flags = +preauth
    }
```
configurar el kadm5.acl --> es para los permisos de los principals (users del kerberos), no exite el fichero, lo creas tu y escribe lo que quieras de los users
```
*/admin@EDT.ORG *
superxaxi@EDT.ORG *
marta@EDT.ORG *
```
```
* --> todos
/algo --> es un rol
*/admin@EDT.ORG * --> todos los users con el rol admin tienen todos los permisos
marta@EDT.ORG * --> marta tiene todos los permisos (user privilegiado)
(mirar man de esto para mas sintaxis de permisos("solo lectura","escritura", etc.))
```




kadmin.local -q "addprincs use/role"
kadmin.local -q "listprincs"

kadmin.local (a secas) --> entra en interpret interactiu y asi no tienes que hacer el -q para query

delprinc user
? --> help


vim /etc/krb5kdc/kadm5.acl --> escribir:

*/admin@EDT.ORG * --> todo principal que tenga el rol "admin" tiene  todos los permisos
superxaxi@EDT.ORG * --> el principal que se llama "superxaxi" tiene todo los permisos
marta@EDT.ORG * --> el principal "marta" tiene todos los permisos

=======
service krb5-admin-server start
service krb5-kdc start -->

nmap localhost --> comprobar que tenemos un server kerberos funcionando 

kinit user --> pedir ticket
kdestroy --> destruir ticket
klist --> listar los tickets que tienes

kinit -p pere/admin
