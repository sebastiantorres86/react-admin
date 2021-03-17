# react-admin

Un framework para crear aplicaciones de administración que se ejecutan en el navegador, además de las API REST/GraphQL, utilizando ES6, [React](https://reactjs.org/) y [Material Design](https://material.io/) . De código abierto y mantenido por [marmelab](https://marmelab.com/).

## Instalación

React-admin está disponible en npm. Puede instalarlo (y sus dependencias requeridas) usando:

```bash
npm install react-admin
#o
yarn add react-admin
```

## Uso

Lea el [tutorial]() para una introducción de 30 minutos. Después de eso, continúe leyendo la [documentación]() o consulte el [código fuente de la demostración](https://github.com/marmelab/react-admin/tree/master/examples/demo) para ver un ejemplo de uso.

## Da un vistazo

```javascript
// en app.js
import * as React from "react";
import { render } from "react-dom";
import { Admin, Resource } from "react-admin";
import simpleRestProvider from "ra-data-simple-rest";

import { PostList, PostEdit, PostCreate, PostIcon } from "./posts";

render(
  <Admin dataProvider={simpleRestProvider("http://localhost:3000")}>
    <Resource
      name="posts"
      list={PostList}
      edit={PostEdit}
      create={PostCreate}
      icon={PostIcon}
    />
  </Admin>,
  document.getElementById("root")
);
```

El componente <Resource> es un componente de configuración que permite definir los subcomponentes para cada una de la vista de administración: `list`, `edit`, y `create`. Estos componentes utilizan Material UI y componentes personalizados de react-admin:

```javascript
// en posts.js

import * as React from "react";
import {
  List,
  Datagrid,
  Edit,
  Create,
  SimpleForm,
  DateField,
  TextField,
  EditButton,
  TextInput,
  DateInput,
} from "react-admin";
import BookIcon from "@material-ui/icons/Book";
export const PostIcon = BookIcon;

export const PostList = (props) => (
  <List {...props}>
    <Datagrid>
      <TextField source="id" />
      <TextField source="title" />
      <DateField source="published_at" />
      <TextField source="average_note" />
      <TextField source="views" />
      <EditButton basePath="/posts" />
    </Datagrid>
  </List>
);

const PostTitle = ({ record }) => {
  return <span>Post {record ? `"${record.title}"` : ""}</span>;
};

export const PostEdit = (props) => (
  <Edit title={<PostTitle />} {...props}>
    <SimpleForm>
      <TextInput disabled source="id" />
      <TextInput source="title" />
      <TextInput source="teaser" options={{ multiline: true }} />
      <TextInput multiline source="body" />
      <DateInput label="Publication date" source="published_at" />
      <TextInput source="average_note" />
      <TextInput disabled label="Nb views" source="views" />
    </SimpleForm>
  </Edit>
);

export const PostCreate = (props) => (
  <Create title="Create a Post" {...props}>
    <SimpleForm>
      <TextInput source="title" />
      <TextInput source="teaser" options={{ multiline: true }} />
      <TextInput multiline source="body" />
      <TextInput label="Publication date" source="published_at" />
      <TextInput source="average_note" />
    </SimpleForm>
  </Create>
);
```

## ¿Funciona con mi API?

Si.

React-admin utiliza un enfoque de adaptador, con un concepto llamado _Data Providers_. Los proveedores existentes se pueden utilizar como modelo para diseñar su API, o puede escribir su propio proveedor de datos para consultar una API existente. Escribir un proveedor de datos personalizado es cuestión de horas.

![](images/data-provider.png)

Consulte la [documentación de data providers]() para obtener más detalles.

## Baterías incluidas pero extraíbles

React-admin está diseñado como una biblioteca de componentes React débilmente acoplados construidos sobre [material-ui](https://material-ui.com/), además de las funciones del controlador implementadas al modo Redux. Es muy fácil reemplazar una parte de react-admin por la suya propia, por ejemplo, para usar un Datagrid personalizado, GraphQL en lugar de REST o bootstrap en lugar de Material Design.

## Apoyo

Puede obtener soporte profesional de Marmelab a través de [React-Admin Enterprise Edition](https://marmelab.com/ra-enterprise), o soporte de la comunidad a través de [StackOverflow](https://stackoverflow.com/questions/tagged/react-admin).

## Contribuyendo

Si quieres echar una mano: ¡Gracias! Hay muchas cosas que puede hacer para ayudar a mejorar react-admin.

La tarea más sencilla es la **clasificación de errores**. Verifique que los nuevos problemas en GitHub sigan la plantilla de problemas y brinden una forma de reproducir el problema. Si no es así, comente el tema para pedir precisiones. Luego, intente reproducir el problema siguiendo la descripción. Si logró reproducir el problema, agregue un comentario para decirlo. De lo contrario, agregue un comentario para decir que falta algo.

La segunda forma de contribuir es **responder preguntas de soporte en** [StackOverflow](https://stackoverflow.com/questions/tagged/react-admin). Hay muchas preguntas para principiantes allí, por lo que incluso si no tiene mucha experiencia con react-admin, hay alguien a quien puede ayudar allí.

Las **pull request** para **correcciones de errores** son bienvenidas en el [repositorio de GitHub](https://github.com/marmelab/react-admin). Siempre hay un montón de problemas etiquetados [como "Buen primer problema"](https://github.com/marmelab/react-admin/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22) en el rastreador de errores; comience con estos. Consulte las pautas de contribución en [el repositorio README](https://github.com/marmelab/react-admin#contributing).

Si desea **agregar una función**, puede abrir una pull request en la rama `next`. No aceptamos todas las funciones; intentamos que el código react-admin sea pequeño y manejable. Pruebe y vea si su función se puede construir como un paquete `npm` adicional . Si tiene dudas, abra un problema de "Feature request" para ver si el equipo central acepta su función antes de desarrollarla.

## Licencia

React-admin tiene la [licencia MIT](https://github.com/marmelab/react-admin/blob/master/LICENSE.md), patrocinada y respaldada por [marmelab](https://marmelab.com/).

## Donar

Esta biblioteca es de uso gratuito, incluso con fines comerciales. Si desea retribuir, hable sobre ello, ayude a los recién llegados o contribuya con el código. Pero la mejor manera de retribuir es **donando a una organización benéfica**. Recomendamos [Médicos sin Fronteras](https://www.doctorswithoutborders.org/).
