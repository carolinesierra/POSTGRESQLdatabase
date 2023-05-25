# POSTGRESQLdatabase

## create user usuariopp;

- Privilegio de SELECT en todas las tablas del esquema publico al usuariopp

    `GRANT SELECT ON ALL TABLES IN SCHEMA public to usuariopp;`

- Se crea la vista llamada {function_source_code} que contiene el nombre de la función y el código fuente para todas las funciones y procedimientos almacenados en el esquema publico. Luego, se otorga el privilegio SELECT en esta vista 
-- creada al usuariopp

    `CREATE OR REPLACE VIEW public.function_source_code AS
    SELECT proname AS function_name, pg_get_functiondef(p.oid)
    FROM pg_proc p 
    JOIN pg_namespace n ON p.pronamespace = n.oid
    WHERE n.nspname = 'public';
    GRANT SELECT ON public.function_source_code TO usuariopp;`

- Antes de exportar la bdd. Si se desea otorgar el privilegio EXECUTE en funciones, se necesita usar la siguiente consulta reemplazando {function_name} con el nombre de la funcion y {parameter_types} con los tipose de parametros requeridos 

`GRANT EXECUTE ON FUNCTION function_name(parameter_types) TO usuariopp;`
