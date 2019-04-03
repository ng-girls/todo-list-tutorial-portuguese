# Refatorando o App Component

Vamos realizar uma pequena refatoração. O componente principal do aplicativo não deve ter um HTML tão grande e com toda essa lógica. Deve apenas chamar outro componente que irá lidar com isso.

* Crie um novo componente chamado `list-manager`:

`ng g c list-manager -it`

* Mova todo o código do `appComponent` para `listManager`
* Referencie o novo componente de dentro do template do `appComponent`:

```
`
  <todo-list-manager></todo-list-manager>
`
```

Só isso! Agora podemos continuar.
