## Integración con stripe
1. Crear una cuenta en [stripe](https://dashboard.stripe.com/test/dashboard) 
2. Obtener la API secret key del [link](https://dashboard.stripe.com/apikeys) y colocarlo en el `.env`
3. Instalar stripe con el comando `npm install stripe --save` [documentación](https://docs.stripe.com/sdks)
4. Configurar la variable de entorno en `config/envs.ts`
### Para embiente local
5. Instalar [CLI de stripe](https://docs.stripe.com/stripe-cli#install) con el comando `docker run --rm -it stripe/stripe-cli:latest`
6. Generar un forward (reenvio) a la ruta local que estará escuchando el webhook con el comando `stripe listen --forward-to localhost:3000/payments/webhook` [link](https://dashboard.stripe.com/test/workbench/webhooks)
7. Activar eventos en el CLI con la finalidad de probar que esten llegando los eventos `stripe trigger payment_intent.succeeded` [link](https://dashboard.stripe.com/test/workbench/webhooks)
### Fin
8. Colocar el raw body en true

```
// main.ts
  const app = await NestFactory.create(AppModule, {
    rawBody: true,
  });
```
9. Para obtener el endpoint Secret para probar en entorno local ejecutar el siguiente comando `stripe listen`