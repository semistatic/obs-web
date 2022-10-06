<script>
    import { onMount } from 'svelte'
    import { obs, sendCommand } from './obs.js'
  
    let inputs = []
    let currentProfile = ''
  
    onMount(async function () {
      const data = await sendCommand('GetSceneItemList', {sceneName:'Scene'})
      inputs = data.sceneItems || []
    //  console.log(inputs)
    })

    obs.on('SceneItemTransformChanged', async (data) => {
      console.log('SceneItemTransformChanged', data.scene.sceneItems)
      inputs = data.sceneItems || []
    })
  
    async function setPositionScene (event) {
     // sendCommand('SetCurrentProfile', { profileName: event.target.value })
     console.log(event.target.value)
    }
  </script>
  
  <div class="select" style="margin: 0 .5rem .5rem 0;">
    <select title="Change Position" on:change={setPositionScene}>
    {#each inputs as input}
      <option value={input.sceneItemId}>{input.sourceName}</option>
    {/each}
    </select>
  </div>
  