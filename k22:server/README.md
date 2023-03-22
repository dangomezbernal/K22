# K22
configurar el krb
configurar el krdc



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
