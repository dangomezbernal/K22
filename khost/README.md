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

kinit user --> pedir ticket (cuando te logeas, automaticamente te da un ticket tmb asi que un poco xd)
kdestroy --> destruir ticket
klist --> listar los tickets que tienes

kinit -p pere/admin
========================
client

instalar el paquete cliente

modificar el fichero de config /etc/krb5.conf --> lo mismo que en el server, hay que especificarle a que realm pertenece, en este caso EDT.ORG

cualquier host que pertenezca al kingdom(realm) puede conectarse al server y hacer cosas

pam

vim /etc/pam.d/common-auth
auth sufficient pam_krb5.so


account sufficient pam_krb5.so

session sufficient pam_krb5.so
