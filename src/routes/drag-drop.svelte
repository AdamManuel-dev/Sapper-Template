<script>
  import {flip} from "svelte/animate";
  import {dndzone} from "svelte-dnd-action";
  import {
    Card,
    CardTitle,
    CardSubtitle,
    CardActions,
    Button,
    Row,
    Col,
  } from 'svelte-materialify/src';

  let items = [
    { id:1, name: 'Tuba Angel', author: 'Иοκτцяηаι', color: 'blue' },
    { id:2, name: 'Tuba Mech', author: 'Noah Giesler', color: 'red' },
    { id:3, name: 'Tuba Archmage', author: 'Noah Giesler', color: 'green' },
  ];

  const flipDurationMs = 300;
  function handleDndConsider(e: any) {
      items = e.detail.items;
  }
  function handleDndFinalize(e: any) {
      items = e.detail.items;
  }
</script>

<div class="justify-center mt-4 mb-4 d-flex">
  <div class="w-full h-full" use:dndzone="{{items, flipDurationMs}}" on:consider="{handleDndConsider}" on:finalize="{handleDndFinalize}">
    {#each items as item (item.id)}
      <div animate:flip="{{duration: flipDurationMs}}" class="outline-none">
        <Card class={item.color}>
          <Row>
            <Col cols={8}>
              <CardTitle>{item.name}</CardTitle>
              <CardSubtitle>{item.author}</CardSubtitle>
              <CardActions>
                <Button text>Play</Button>
              </CardActions>
            </Col>
            <Col cols={4}><img src="//picsum.photos/100?random={item.id}" alt="cover" /></Col>
          </Row>
        </Card>
      </div>
    {/each}
  </div>
</div>