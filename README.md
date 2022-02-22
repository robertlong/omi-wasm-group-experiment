# OMI WASM Group Experiment

Robert Long - Matrix.org

## Proposal

[Experiment Project 1 Proposal](https://github.com/omigroup/omi-wasm-group/discussions/19)

I'm still working on the implementation for this. But here's the general API I'm looking to produce in AssemblyScript:

```typescript
getEventQueue(Physics, Physics.intersectionEvents): IntersectionEvent[]

interface IntersectionEvent {
  trigger: u32
  collider: u32
  intersecting: bool
}

getEntityByName("Audio Emitter"): u32

getPropertyStoreBool(AudioEmitter, AudioEmitter.playing): bool[]
getPropertyStoreVec3(Material, Material.color): vec3[]
getPropertyStoreVec3(Transform, Transform.position): vec3[]
getPropertyStoreVec3(Transform, Transform.rotation): euler[]
getPropertyStoreVec3(Transform, Transform.quaternion): quat[]
getPropertyStoreVec3(Transform, Transform.scale): vec3[]
getPropertyStoreVec3(Transform, Transform.localMatrix): mat4[]
getPropertyStoreVec3(Transform, Transform.worldMatrix): mat4[]
getPropertyStoreVec3(Transform, Transform.worldMatrixNeedsUpdate): bool[]
getPropertyStoreVec3(Transform, Transform.parent): u32[]
getPropertyStoreVec3(Transform, Transform.first_child): u32[]
getPropertyStoreVec3(Transform, Transform.prev_sibling): u32[]
getPropertyStoreVec3(Transform, Transform.next_sibling): u32[]

// Example 1: Play a sound

const audioEmitterEid = getEntityByName("Audio Emitter");
const intersectionEventQueue = getEventQueue(Physics, Physics.intersectionEvents);
const playing = getPropertyStoreBool(AudioEmitter, AudioEmitter.playing);

for (const event of intersectionEventQueue) {
  if (event.collider === audioEmitterEid) {
    playing[audioEmitterEid] = event.intersecting;
  }
}

// Example 2: Change a material color

const  = getEntityByName("Red Cube");
const intersectionEventQueue = getEventQueue(Physics, Physics.intersectionEvents);
const color = getPropertyStoreVec3(Material, Material.color);

for (const event of intersectionEventQueue) {
  if (event.collider === cubeEid) {
    color[cubeEid] = event.intersecting ? vec3(1, 0, 0) : vec3(0, 0, 1);
  }
}

// Example 2: Transforms

const spinningCubeEid = getEntityByName("Spinning Cube");
const intersectionEventQueue = getEventQueue(Physics, Physics.intersectionEvents);
const rotation = getPropertyStoreVec3(Transform, Transform.rotation): euler[]

for (const event of intersectionEventQueue) {
  if (event.collider === spinningCubeEid) {
    rotation[cubeEid].y += event.intersecting ? 0.5 : 0;
  }
}
```