# Unity & JavaScript Toolbox

A concise, practical README focused on Unity development and JavaScript tooling — compact tips, the Unity version used, a clean example AI helper, and recommended workflows for Unity multiplayer projects.

[![Unity 6000.0.34f1](https://img.shields.io/badge/Unity-6000.0.34f1-blue.svg)]()
[![Photon PUN](https://img.shields.io/badge/Photon-PUN-orange.svg)]()

About
- This repo (or template) is centered on Unity development and complementary JavaScript tooling.
- Use Unity for real-time game logic, rendering, physics, AI and networking; use JavaScript for editor tooling, build pipelines, web frontends, or Node-based servers and utilities.
- Photon PUN experience: 3+ years working with PUN for multiplayer synchronization and room logic.

Quick setup
- Clone and open with Unity Hub using the matching Editor version (6000.0.34f1).
- Recommended: enable Visible Meta Files and Force Text serialization (Edit → Project Settings → Editor).
- Use Git LFS for large binary assets (textures, audio, models).

Compact tips
- Use Vector3.SqrMagnitude for distance comparisons when possible to avoid costly sqrt.
- Cache frequently queried objects (avoid FindGameObjectsWithTag every frame).
- Keep gameplay state deterministic where possible and reconcile via Photon for smooth multiplayer.
- JavaScript is excellent for: editor automation (node + CLI + npm scripts), web dashboards, remote tools, and lightweight server tasks.

Sample C# helper (Find nearest player)
- Cleaned and annotated version of the provided function. It finds the nearest GameObject tagged "Player" that has a PhotonView, with optional distance gating and performance-friendly suggestions.

```csharp
using UnityEngine;
using Photon.Pun;

public class EnemyAI : MonoBehaviour
{
    public float keepPatrolDistance = 10f;
    public bool isChasing = false;

    // Returns the Transform of the nearest player (or null).
    Transform FindNearestPlayer()
    {
        var players = GameObject.FindGameObjectsWithTag("Player");
        float bestDistSq = Mathf.Infinity;
        Transform best = null;
        Vector3 myPos = transform.position;

        foreach (var p in players)
        {
            if (p == null) continue;

            var pv = p.GetComponent<PhotonView>();
            if (pv == null) continue;

            // Use squared distance for performance
            float distSq = (p.transform.position - myPos).sqrMagnitude;

            // Skip players outside patrol range when not chasing
            float keepDistSq = keepPatrolDistance * keepPatrolDistance;
            if (!isChasing && distSq > keepDistSq) continue;

            if (distSq < bestDistSq)
            {
                bestDistSq = distSq;
                best = p.transform;
            }
        }

        return best;
    }
}
```

Performance notes
- For frequent checks, maintain a list of active player Transforms (update on join/leave) instead of calling FindGameObjectsWithTag().
- Consider running expensive scans at intervals (e.g., every 0.2–0.5s) instead of every frame.
- If using Unity NavMesh for AI, combine nearest-player selection with navmesh path distance checks for better chasing behavior.

JavaScript (JS) usage ideas
- Editor automation: Node.js scripts to mass-edit assets, generate config files, or run precommit checks.
- Build & deploy: npm scripts for automated packaging, exporting asset bundles, or CI tasks.
- Web frontends: dashboards for game server status, player metrics, or remote configuration panels.
- Server side: lightweight Node services for matchmaking telemetry or external webhooks.

Fantastic possibilities (short)
- Procedural terrains and structures synced across clients with PUN events.
- AI that plans and stalks players using combined navmesh pathing + predictive movement.
- Web-based admin tools (JS) to inspect live matches and trigger dynamic events.

Repository layout suggestion
- Assets/ — Unity runtime code, prefabs, scenes
- Assets/Samples/ — demo scenes
- Packages/ — optional UPM layout
- .github/ — workflows, templates, social-preview
- tools/ or scripts/ — JavaScript tooling and build scripts
- docs/ — short docs and setup notes

License & contact
- Choose a license (MIT recommended for open source). Add LICENSE at repo root.
- Maintainer: @TLIdoc

If you want, I can:
- Trim or expand any section,
- Convert JS ideas into starter Node scripts,
- Add a small GitHub Action to run Unity tests or build player artifacts.
