# AGENT EXECUTION RUNBOOK: 100% Free Automated 90s AI Reel Pipeline

> **TARGET READER:** Autonomous Coding Agent / Lower-Tier LLM Executor
>
> **EXECUTION MODE:** Strict, Linear, Deterministic (Zero Hallucination Tolerance)
>
> **ARCHITECTURE PHILOSOPHY:** Karpathy Guidelines (*Think Before Coding, Simplicity First, Surgical Execution, Goal-Driven Verification*)

---

## 0. STRICT SYSTEM GUARDRAILS (READ FIRST)

You are an execution agent tasked with setting up, verifying, and scheduling a **100% free-forever automated Instagram Reel production workline**. Follow these rules literally:

1. **NO EXTRA DEPENDENCIES:** Do **NOT** install `moviepy`, `opencv-python`, `langchain`, `boto3`, `cloudinary`, or `instagrapi`. You may ONLY install `edge-tts` and `gradio_client` via `pip`, plus system `ffmpeg`.
2. **NO MULTI-FILE ABSTRACTION:** Keep all Python logic inside a single file named `auto_reel.py`. Do not split code into helper modules or classes.
3. **MANDATORY VERIFICATION GATES:** You **MUST** run the exact verification command after each phase. If a command returns a non-zero exit code, **STOP** and consult **Section 7 (Deterministic Troubleshooting Matrix)**. Do not guess or invent workarounds.
4. **CHARACTER CONSISTENCY:** Every Reel must use a locked `character_anchor` string prepended to every scene's image prompt so the protagonist looks identical across all shots.
5. **COPYRIGHT-SAFE PROCEDURAL AUDIO:** Do not download external copyrighted MP3s. Use the built-in FFmpeg procedural 90s warm tape-synth generator mixed under the neural voiceover.

---

## 1. COMPLETE WEBSITE DIRECTORY, LOGINS & WORKAROUNDS

Below is every website and endpoint used by this pipeline, whether a login is required, and the exact technical workaround built into the system to keep it 100% free forever:

| Stage | Website / Endpoint URL | Login Required? | Free Limit / Bottleneck | Exact Built-In Workaround |
| :--- | :--- | :--- | :--- | :--- |
| **1. Script & Storyboard LLM** | `https://text.pollinations.ai/` | **NO** (Zero Login, Keyless) | Occasional rate-limit (`HTTP 429/502`) or chatty markdown around JSON | **Workaround 1A:** Automatic model fallback loop (`openai` $\rightarrow$ `mistral` $\rightarrow$ `llama`).<br>**Workaround 1B:** Deterministic substring bracket extraction (`raw[raw.find("{"):raw.rfind("}")+1]`) so chatty LLM prefixes never break JSON parsing. |
| **2. 90s 35mm Keyframes** | `https://image.pollinations.ai/` | **NO** (Zero Login, Keyless) | Adds a small bottom-right watermark by default; `flux` model can timeout at peak hours | **Workaround 2A:** Append `&nologo=true&nofeed=true` to strip watermarks without an account.<br>**Workaround 2B:** Auto-fallback from `model=flux` $\rightarrow$ `model=turbo` with a shifted random seed if generation takes $>90$ seconds. |
| **3. Neural Voiceover (TTS)** | Microsoft Edge Neural TTS (`edge-tts` CLI) | **NO** (Zero Login, Keyless) | Standard cloud TTS APIs (ElevenLabs) charge per character | **Workaround 3:** `edge-tts` connects directly to Microsoft Edge's internal browser Read-Aloud WebSocket for unlimited free neural audio (`en-US-AvaNeural`). |
| **4. True AI Motion (I2V)** | `https://huggingface.co/spaces/Lightricks/LTX-Video`<br>Token Page: `https://huggingface.co/settings/tokens` | **OPTIONAL** (Works without login; free HF account increases quota) | Public ZeroGPU Spaces enforce a daily IP compute quota (~5 mins of H200 GPU time/day per IP) | **Workaround 4A:** Pass a free Read-Only `HF_TOKEN` from `huggingface.co/settings/tokens` to double your daily ZeroGPU quota.<br>**Workaround 4B:** If ZeroGPU quota is exhausted, `auto_reel.py` automatically falls back to the local **FFmpeg 35mm Pan/Zoom + Kodak Film Grain Engine** so the daily post never fails. |
| **5. Direct Video Hosting** | `https://rupload.facebook.com/ig-api-upload/v22.0/` | **YES** (Uses your free Meta Token) | Standard Instagram API requires a paid S3/Cloudinary public URL to fetch videos | **Workaround 5:** Use Meta's undocumented/underused `upload_type=resumable` endpoint on `rupload.facebook.com` to stream the local `.mp4` binary directly from disk—zero cloud storage needed. |
| **6. Instagram Auto-Publish** | `https://developers.facebook.com/apps`<br>`https://business.facebook.com/settings/system-users` | **YES** (Free IG Creator Account + Free Meta Dev Account) | Standard tokens expire after 1 hour or 60 days; linking a Facebook Page can be annoying | **Workaround 6A (No FB Page Needed):** Use *Instagram API with Instagram Login* inside your Meta App.<br>**Workaround 6B (Never-Expiring Token):** Generate a **System User Access Token** in Meta Business Settings—it **never expires** ($0$ maintenance forever). See Section 6 for exact clicks. |
| **7. Cloud Cron Scheduler** | `https://github.com/` (GitHub Actions) | **YES** (Free GitHub Account) | GitHub Actions automatically disables scheduled `cron` workflows after 60 days of repo inactivity | **Workaround 7:** Every daily run commits the updated `state.json` queue back to the repo (`git commit` + `git push`), which resets GitHub's 60-day activity timer indefinitely. |

---

## PHASE 1: Environment & Dependency Setup

### Step 1.1: Create Workspace Directory

Run this exact command in the terminal:

```bash
mkdir -p auto_reel_workline/.github/workflows && cd auto_reel_workline
```

### Step 1.2: Install System FFmpeg & Python Packages

Detect the OS and execute the matching block:

**On Linux (Ubuntu/Debian):**

```bash
sudo apt-get update -y && sudo apt-get install -y ffmpeg fonts-dejavu-core python3-pip python3-venv
python3 -m venv .venv
.venv/bin/pip install --upgrade pip edge-tts gradio_client
```

**On macOS:**

```bash
brew install ffmpeg
python3 -m venv .venv
.venv/bin/pip install --upgrade pip edge-tts gradio_client
```

**On Windows (PowerShell):**

```powershell
winget install Gyan.FFmpeg
python -m venv .venv
.\.venv\Scripts\pip install --upgrade pip edge-tts gradio_client
```

### VERIFICATION GATE 1 (Mandatory)

Run this command and confirm the output contains `GATE_1_OK`:

```bash
ffmpeg -version >/dev/null 2>&1 && ffprobe -version >/dev/null 2>&1 && .venv/bin/edge-tts --version >/dev/null 2>&1 && echo "GATE_1_OK"
```

*(On Windows, replace `.venv/bin/edge-tts` with `.\.venv\Scripts\edge-tts.exe`)*

---

## PHASE 2: Create the Autonomous Theme Queue (`state.json`)

To operate as an autonomous workline without repeating videos, create `state.json` in the project root. The script pops the next unposted theme, or auto-generates a new 90s adventure plot if the queue empties.

Write the exact contents below to `state.json`:

```json
{
  "last_token_refresh_epoch": 0,
  "completed_count": 0,
  "theme_queue": [
    "Three best friends in a 1995 red convertible driving down the Pacific Coast Highway at sunset to forget a breakup",
    "Two childhood friends running through a neon-lit 1990s Tokyo arcade during a midnight rainstorm",
    "A solo girl in a vintage leather jacket boarding an overnight 1990s European sleeper train with a disposable camera",
    "Four friends on a 1990s Manhattan rooftop diner sharing milkshakes as the city lights flicker on at dusk",
    "Best friends sneaking into a 1990s drive-in movie theater in the back of a station wagon with fairy lights"
  ]
}
```

### VERIFICATION GATE 2 (Mandatory)

Run this command and confirm the output is `GATE_2_OK`:

```bash
python3 -c "import json; d=json.load(open('state.json')); assert len(d['theme_queue'])>=1; print('GATE_2_OK')"
```

---

## PHASE 3: Write the Single-File Production Engine (`auto_reel.py`)

Write the exact contents below to `auto_reel.py`. It includes all model fallbacks, JSON bracket extraction, watermark stripping (`nologo=true`), ZeroGPU space rotation, and direct binary uploading.

```python
#!/usr/bin/env python3
"""
auto_reel.py — Autonomous Zero-Cost 90s AI Mini-Movie Workline.
100% Free Forever: Pollinations (Text/Flux) + HF ZeroGPU/FFmpeg 35mm Engine + Edge-TTS + IG Graph API.
Includes multi-model fallbacks, watermark stripping, and JSON bracket extraction workarounds.
"""

import json
import os
import random
import shutil
import subprocess
import sys
import time
import urllib.error
import urllib.parse
import urllib.request
from pathlib import Path

ROOT_DIR = Path(__file__).resolve().parent
STATE_FILE = ROOT_DIR / "state.json"
WORK_DIR = ROOT_DIR / "build_reel"
OUTPUT_MP4 = ROOT_DIR / "final_reel.mp4"

VOICE = "en-US-AvaNeural"
STYLE_SUFFIX = (
    ", 1990s 35mm movie still, Kodak Portra 400 film stock, heavy vintage film grain, "
    "anamorphic lens flare, warm nostalgic color grading, directed by Wong Kar-wai, vertical 9:16"
)


def log(msg: str) -> None:
    print(f"[{time.strftime('%Y-%m-%d %H:%M:%S')}] {msg}", flush=True)


def run_cmd(cmd: list[str], step_name: str) -> str:
    res = subprocess.run(cmd, capture_output=True, text=True)
    if res.returncode != 0:
        raise RuntimeError(f"[{step_name} FAILED]\nCMD: {' '.join(cmd)}\nSTDERR: {res.stderr.strip()}")
    return res.stdout.strip()


def http_request_with_retry(req: urllib.request.Request, retries: int = 4, timeout: int = 90) -> bytes:
    for attempt in range(1, retries + 1):
        try:
            with urllib.request.urlopen(req, timeout=timeout) as resp:
                return resp.read()
        except Exception as exc:
            if attempt == retries:
                raise RuntimeError(f"HTTP failed after {retries} attempts for {req.full_url}: {exc}") from exc
            wait = attempt * 5
            log(f"HTTP retry {attempt}/{retries} in {wait}s ({exc})...")
            time.sleep(wait)
    return b""


# ---------------------------------------------------------------------------
# STEP 1: Load Queue State & Auto-Refresh 60-Day Instagram Token
# ---------------------------------------------------------------------------
def load_and_pop_theme() -> tuple[str, dict]:
    if not STATE_FILE.exists():
        STATE_FILE.write_text(json.dumps({
            "last_token_refresh_epoch": 0,
            "completed_count": 0,
            "theme_queue": ["Best friends on a 1990s midnight road trip turning heartbreak into an adventure"]
        }, indent=2))

    state = json.loads(STATE_FILE.read_text())
    queue = state.get("theme_queue", [])
    if queue:
        theme = queue.pop(0)
    else:
        decades = ["1994", "1996", "1998", "1999"]
        settings = ["coastal diner", "neon bowling alley", "Parisian rooftop", "desert motel pool", "record store"]
        theme = f"Best friends in {random.choice(decades)} hanging out at a {random.choice(settings)} turning heartbreak into an adventure"
    return theme, state


def save_state(state: dict) -> None:
    state["completed_count"] = state.get("completed_count", 0) + 1
    STATE_FILE.write_text(json.dumps(state, indent=2))


def maybe_refresh_ig_token(state: dict) -> str | None:
    token = os.environ.get("IG_ACCESS_TOKEN")
    if not token:
        return None
    now = int(time.time())
    if now - state.get("last_token_refresh_epoch", 0) < 2_160_000:
        return token
    try:
        params = urllib.parse.urlencode({
            "grant_type": "ig_refresh_token",
            "access_token": token,
        })
        url = f"https://graph.instagram.com/refresh_access_token?{params}"
        req = urllib.request.Request(url, headers={"User-Agent": "AutoReel/1.0"})
        raw = json.loads(http_request_with_retry(req, retries=2, timeout=30).decode("utf-8"))
        if "access_token" in raw:
            log("Refreshed Instagram Long-Lived Token (+60 days).")
            state["last_token_refresh_epoch"] = now
            return raw["access_token"]
    except Exception as exc:
        log(f"Token refresh skipped (System User tokens do not need refresh): {exc}")
    return token


# ---------------------------------------------------------------------------
# STEP 2: Storyboard Generation with Multi-Model & Bracket Extraction Workaround
# ---------------------------------------------------------------------------
def generate_storyboard(theme: str) -> dict:
    log(f"Generating 4-scene 90s storyboard for theme: {theme}")
    system_prompt = (
        "You are a 1990s indie film director. Output ONLY valid raw JSON (no markdown fences). "
        "Required schema: "
        '{"character_anchor": "concise physical description of lead character hair, face, and 90s outfit", '
        '"caption": "emotional Instagram caption + #storytelling #aifilmmaking #90saesthetic #aivideo", '
        '"scenes": [{"narration": "max 14 words spoken line", "visual_prompt": "action, setting, camera angle"}]} '
        "Must contain exactly 4 scenes."
    )

    models_to_try = ["openai", "mistral", "llama"]
    last_err = None

    for model_name in models_to_try:
        try:
            payload = json.dumps({
                "messages": [
                    {"role": "system", "content": system_prompt},
                    {"role": "user", "content": f"Create a 4-scene 90s movie Reel about: {theme}"},
                ],
                "model": model_name,
                "seed": random.randint(1, 99999),
                "jsonMode": True,
            }).encode("utf-8")

            req = urllib.request.Request(
                "https://text.pollinations.ai/",
                data=payload,
                headers={"Content-Type": "application/json", "User-Agent": "AutoReel/1.0"},
            )
            raw_text = http_request_with_retry(req, retries=3, timeout=60).decode("utf-8").strip()

            # Workaround 1B: Extract exact JSON object between outer curly braces
            start_idx = raw_text.find("{")
            end_idx = raw_text.rfind("}")
            if start_idx != -1 and end_idx != -1:
                raw_text = raw_text[start_idx : end_idx + 1]

            data = json.loads(raw_text)
            assert "scenes" in data and len(data["scenes"]) >= 2, "Storyboard missing scenes list"
            assert "character_anchor" in data, "Storyboard missing character_anchor"
            log(f"[VERIFY] Storyboard ready via model='{model_name}' ({len(data['scenes'])} scenes).")
            return data
        except Exception as exc:
            last_err = exc
            log(f"Model '{model_name}' failed to produce valid JSON ({exc}), trying fallback model...")

    raise RuntimeError(f"All free LLM models failed to generate storyboard: {last_err}")


# ---------------------------------------------------------------------------
# STEP 3: Keyframe Generation (Flux -> Turbo Workaround) + Optional ZeroGPU I2V
# ---------------------------------------------------------------------------
def fetch_keyframe(character_anchor: str, scene_prompt: str, out_jpg: Path, seed: int) -> None:
    combined_prompt = f"{character_anchor}, {scene_prompt}{STYLE_SUFFIX}"
    encoded = urllib.parse.quote(combined_prompt)

    # Workaround 2A & 2B: Strip watermarks (nologo=true) and fallback flux -> turbo on timeout
    for img_model in ["flux", "turbo"]:
        try:
            url = (
                f"https://image.pollinations.ai/prompt/{encoded}"
                f"?width=1080&height=1920&seed={seed}&model={img_model}&nologo=true&nofeed=true"
            )
            req = urllib.request.Request(url, headers={"User-Agent": "AutoReel/1.0"})
            img_bytes = http_request_with_retry(req, retries=3, timeout=90)
            out_jpg.write_bytes(img_bytes)
            if out_jpg.exists() and out_jpg.stat().st_size > 15_000:
                return
        except Exception as exc:
            log(f"Image model '{img_model}' timed out ({exc}); trying fallback...")
            seed += 101

    raise RuntimeError(f"Failed to generate keyframe for {out_jpg}")


def try_hf_zerogpu_i2v(image_path: Path, prompt: str, out_mp4: Path) -> bool:
    if os.environ.get("USE_HF_ZEROGPU", "0") != "1":
        return False
    try:
        from gradio_client import Client, handle_file
        hf_token = os.environ.get("HF_TOKEN")  # Optional free token to double ZeroGPU quota
        client = Client("Lightricks/LTX-Video", token=hf_token)
        res = client.predict(
            prompt=prompt + STYLE_SUFFIX,
            input_image_filepath=handle_file(str(image_path)),
            height=768,
            width=512,
            num_frames=65,
            api_name="/image_to_video",
        )
        video_file = res[0] if isinstance(res, (list, tuple)) else res
        shutil.copy(video_file, out_mp4)
        return out_mp4.exists() and out_mp4.stat().st_size > 30_000
    except Exception as exc:
        log(f"ZeroGPU IP quota reached or busy ({exc}); using deterministic FFmpeg 35mm film engine.")
        return False


def find_edge_tts_bin() -> str:
    venv_bin = ROOT_DIR / ".venv" / ("Scripts/edge-tts.exe" if os.name == "nt" else "bin/edge-tts")
    if venv_bin.exists():
        return str(venv_bin)
    return "edge-tts"


def render_scene(idx: int, character_anchor: str, scene: dict, base_seed: int) -> Path:
    img_path = WORK_DIR / f"scene_{idx}.jpg"
    tts_path = WORK_DIR / f"scene_{idx}_tts.mp3"
    mixed_aud_path = WORK_DIR / f"scene_{idx}_mixed.m4a"
    raw_i2v_path = WORK_DIR / f"scene_{idx}_i2v.mp4"
    final_scene_mp4 = WORK_DIR / f"scene_{idx}_final.mp4"

    # 1. Neural Voiceover via edge-tts
    run_cmd(
        [find_edge_tts_bin(), "--voice", VOICE, "--text", scene["narration"], "--write-media", str(tts_path)],
        f"TTS Scene {idx}",
    )
    dur_str = run_cmd(
        ["ffprobe", "-v", "error", "-show_entries", "format=duration", "-of", "default=noprint_wrappers=1:nokey=1", str(tts_path)],
        f"Probe TTS Scene {idx}",
    )
    duration = max(float(dur_str) + 0.4, 2.8)
    frames = int(duration * 30)

    # 2. Mix Voiceover with Procedural 90s Warm Analog Synth Pad + Tape Hiss (100% Copyright-Free)
    run_cmd(
        [
            "ffmpeg", "-y",
            "-i", str(tts_path),
            "-f", "lavfi", "-i", f"aevalsrc=0.025*sin(2*PI*110*t)+0.015*sin(2*PI*164.81*t)+0.01*sin(2*PI*220*t):s=44100:d={duration:.2f}",
            "-f", "lavfi", "-i", f"anoisesrc=d={duration:.2f}:c=pink:r=44100:a=0.004",
            "-filter_complex", "[0:a]volume=1.4[vo];[1:a]lowpass=f=400[pad];[vo][pad][2:a]amix=inputs=3:duration=first:dropout_transition=0[aout]",
            "-map", "[aout]", "-c:a", "aac", "-b:a", "192k", str(mixed_aud_path),
        ],
        f"Audio Mix Scene {idx}",
    )

    # 3. Generate Character-Consistent 90s Keyframe
    fetch_keyframe(character_anchor, scene["visual_prompt"], img_path, seed=base_seed + idx)

    # 4. Write Subtitle File (SRT) for Safe Cross-Platform Burn-In
    srt_path = WORK_DIR / f"scene_{idx}.srt"
    srt_path.write_text(f"1\n00:00:00,050 --> 00:00:{duration-0.05:06.3f}\n{scene['narration']}\n".replace(".", ","), encoding="utf-8")
    rel_srt = srt_path.name

    zoom_expr = "min(zoom+0.0012,1.16)" if idx % 2 == 0 else "if(eq(on,1),1.16,max(1.0,zoom-0.0012))"

    used_i2v = try_hf_zerogpu_i2v(img_path, f"{character_anchor}, {scene['visual_prompt']}", raw_i2v_path)
    if used_i2v:
        vf_filter = (
            f"scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920,"
            f"noise=alls=13:allf=t+u,eq=contrast=1.07:saturation=0.90,"
            f"subtitles={rel_srt}:force_style='Fontsize=16,PrimaryColour=&H0000D7FF,OutlineColour=&H00000000,BorderStyle=1,Outline=2,Shadow=1,Alignment=2,MarginV=75'"
        )
        cmd = [
            "ffmpeg", "-y", "-stream_loop", "-1", "-i", str(raw_i2v_path), "-i", str(mixed_aud_path),
            "-t", f"{duration:.2f}", "-vf", vf_filter,
            "-c:v", "libx264", "-pix_fmt", "yuv420p", "-r", "30",
            "-c:a", "copy", "-shortest", str(final_scene_mp4),
        ]
    else:
        vf_filter = (
            f"scale=2160:3840,"
            f"zoompan=z='{zoom_expr}':x='iw/2-(iw/zoom/2)':y='ih/2-(ih/zoom/2)':d={frames}:s=1080x1920:fps=30,"
            f"noise=alls=14:allf=t+u,eq=contrast=1.07:saturation=0.90,"
            f"subtitles={rel_srt}:force_style='Fontsize=16,PrimaryColour=&H0000D7FF,OutlineColour=&H00000000,BorderStyle=1,Outline=2,Shadow=1,Alignment=2,MarginV=75'"
        )
        cmd = [
            "ffmpeg", "-y", "-loop", "1", "-i", str(img_path), "-i", str(mixed_aud_path),
            "-t", f"{duration:.2f}", "-vf", vf_filter,
            "-c:v", "libx264", "-pix_fmt", "yuv420p", "-r", "30",
            "-c:a", "copy", str(final_scene_mp4),
        ]

    res = subprocess.run(cmd, cwd=str(WORK_DIR), capture_output=True, text=True)
    if res.returncode != 0:
        raise RuntimeError(f"Scene {idx} FFmpeg failed:\n{res.stderr.strip()}")
    assert final_scene_mp4.exists() and final_scene_mp4.stat().st_size > 40_000, f"Scene {idx} output too small"
    log(f"[VERIFY] Scene {idx} rendered ({duration:.1f}s).")
    return final_scene_mp4


def assemble_final_reel(scene_files: list[Path], out_mp4: Path) -> None:
    concat_list = WORK_DIR / "concat.txt"
    concat_list.write_text("\n".join(f"file '{p.name}'" for p in scene_files) + "\n", encoding="utf-8")
    res = subprocess.run(
        ["ffmpeg", "-y", "-f", "concat", "-safe", "0", "-i", "concat.txt", "-c", "copy", str(out_mp4)],
        cwd=str(WORK_DIR),
        capture_output=True,
        text=True,
    )
    if res.returncode != 0:
        raise RuntimeError(f"Concat failed:\n{res.stderr.strip()}")

    probe = json.loads(
        run_cmd(
            ["ffprobe", "-v", "error", "-select_streams", "v:0", "-show_entries", "stream=width,height,codec_name,duration", "-of", "json", str(out_mp4)],
            "Final MP4 Probe",
        )
    )
    st = probe["streams"][0]
    assert st["width"] == 1080 and st["height"] == 1920 and st["codec_name"] == "h264", f"Bad video stream: {st}"
    log(f"[VERIFY] Final Reel assembled: {out_mp4} (1080x1920, H.264, {float(st.get('duration', 0)):.1f}s)")


# ---------------------------------------------------------------------------
# STEP 4: Direct Local Binary Upload to Instagram Graph API (Zero S3 Hosting)
# ---------------------------------------------------------------------------
def publish_instagram_resumable(mp4_path: Path, caption: str, access_token: str | None) -> None:
    ig_user_id = os.environ.get("IG_USER_ID")
    if not ig_user_id or not access_token:
        log("[DRY RUN] IG_USER_ID or IG_ACCESS_TOKEN not set. Skipping live Instagram publish.")
        return

    api_ver = "v22.0"
    base_url = f"https://graph.facebook.com/{api_ver}/{ig_user_id}"

    # Workaround 5: Resumable binary upload bypasses the need for AWS S3 or Cloudinary URLs
    init_data = urllib.parse.urlencode({
        "media_type": "REELS",
        "upload_type": "resumable",
        "caption": caption,
        "share_to_feed": "true",
        "has_consumer_generated_ai_content": "true",
        "access_token": access_token,
    }).encode("utf-8")
    req = urllib.request.Request(f"{base_url}/media", data=init_data, method="POST")
    init_res = json.loads(http_request_with_retry(req, retries=3).decode("utf-8"))
    container_id = init_res["id"]
    upload_uri = init_res.get("uri") or f"https://rupload.facebook.com/ig-api-upload/{api_ver}/{container_id}"

    video_bytes = mp4_path.read_bytes()
    up_req = urllib.request.Request(
        upload_uri,
        data=video_bytes,
        method="POST",
        headers={
            "Authorization": f"OAuth {access_token}",
            "offset": "0",
            "file_size": str(len(video_bytes)),
            "Content-Type": "application/octet-stream",
        },
    )
    up_res = json.loads(http_request_with_retry(up_req, retries=3, timeout=180).decode("utf-8"))
    assert up_res.get("success") is True, f"IG binary upload failed: {up_res}"

    for _ in range(30):
        time.sleep(10)
        poll_url = f"https://graph.facebook.com/{api_ver}/{container_id}?fields=status_code,status&access_token={access_token}"
        st = json.loads(http_request_with_retry(urllib.request.Request(poll_url), retries=2).decode("utf-8"))
        code = st.get("status_code")
        log(f"[IG POLL] Container {container_id}: {code}")
        if code == "FINISHED":
            break
        if code in ("ERROR", "EXPIRED"):
            raise RuntimeError(f"IG processing error: {st}")
    else:
        raise TimeoutError("IG container timed out after 300s")

    pub_data = urllib.parse.urlencode({"creation_id": container_id, "access_token": access_token}).encode("utf-8")
    pub_req = urllib.request.Request(f"{base_url}/media_publish", data=pub_data, method="POST")
    pub_res = json.loads(http_request_with_retry(pub_req, retries=3).decode("utf-8"))
    log(f"[PUBLISHED] Live Instagram Reel Media ID: {pub_res['id']}")


def main() -> None:
    if WORK_DIR.exists():
        shutil.rmtree(WORK_DIR)
    WORK_DIR.mkdir(parents=True)

    theme, state = load_and_pop_theme()
    token = maybe_refresh_ig_token(state)
    storyboard = generate_storyboard(theme)

    base_seed = random.randint(1000, 90000)
    clips = [
        render_scene(i, storyboard["character_anchor"], scene, base_seed)
        for i, scene in enumerate(storyboard["scenes"])
    ]
    assemble_final_reel(clips, OUTPUT_MP4)
    publish_instagram_resumable(OUTPUT_MP4, storyboard.get("caption", theme), token)
    save_state(state)
    log("WORKLINE RUN COMPLETE.")


if __name__ == "__main__":
    main()
```

### VERIFICATION GATE 3 (Mandatory End-to-End Dry Run)

Execute a full local dry run (without needing Instagram credentials yet) to prove that storyboard generation, neural TTS, procedural synth audio mixing, Pollinations Flux keyframes, subtitle burn-in, and H.264 assembly all succeed:

```bash
.venv/bin/python3 auto_reel.py
```

Then run this exact verification check:

```bash
ffprobe -v error -select_streams v:0 -show_entries stream=width,height,codec_name -of csv=p=0 final_reel.mp4 | grep -q "h264,1080,1920" && echo "GATE_3_OK"
```

**STOP IF `GATE_3_OK` IS NOT PRINTED.** Consult Section 7 if an error occurs.

---

## PHASE 4: Establish the Autonomous Schedule (Choose 4A or 4B)

### Option 4A: 100% Cloud-Free via GitHub Actions (Recommended)

Write the exact contents below to `.github/workflows/daily_reel.yml`. It runs automatically every day, generates a new 90s AI Reel, posts it to Instagram, and commits `state.json` back to the repository (which also prevents GitHub from disabling the cron schedule after 60 days).

```yaml
name: Autonomous 90s AI Reel Workline

on:
  schedule:
    - cron: '30 12 * * *' # Runs daily at 12:30 UTC (6:00 PM IST)
  workflow_dispatch:

permissions:
  contents: write

jobs:
  produce-and-publish:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Set Up Python 3.12
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      - name: Install System FFmpeg & Python Venv
        run: |
          sudo apt-get update -y && sudo apt-get install -y ffmpeg fonts-dejavu-core
          python3 -m venv .venv
          .venv/bin/pip install --upgrade pip edge-tts gradio_client

      - name: Run Autonomous Reel Pipeline
        env:
          IG_USER_ID: ${{ secrets.IG_USER_ID }}
          IG_ACCESS_TOKEN: ${{ secrets.IG_ACCESS_TOKEN }}
          HF_TOKEN: ${{ secrets.HF_TOKEN }}
          USE_HF_ZEROGPU: "0"
        run: .venv/bin/python3 auto_reel.py

      - name: Upload Generated MP4 Artifact
        uses: actions/upload-artifact@v4
        with:
          name: daily-90s-reel
          path: final_reel.mp4
          retention-days: 7

      - name: Commit Updated Theme Queue State (Prevents 60-Day Cron Timeout)
        run: |
          git config user.name "AutoReel-Bot"
          git config user.email "bot@autoreel.local"
          git add state.json
          git diff --staged --quiet || git commit -m "chore: advance autonomous reel queue [skip ci]"
          git push
```

### Option 4B: Local Machine Daemon (`cron`)

If running on a local Linux/macOS machine instead of GitHub Actions, register the daily cron job idempotently with this exact command:

```bash
(crontab -l 2>/dev/null | grep -v "auto_reel.py"; echo "30 18 * * * cd $(pwd) && $(pwd)/.venv/bin/python3 $(pwd)/auto_reel.py >> $(pwd)/workline.log 2>&1") | crontab -
```

### VERIFICATION GATE 4 (Mandatory)

Verify that either `.github/workflows/daily_reel.yml` exists OR `crontab -l` contains `auto_reel.py`:

```bash
test -f .github/workflows/daily_reel.yml && echo "GATE_4_OK"
```

---

## PHASE 5: Step-by-Step Website Login & Token Workarounds (Human Handoff)

Only **two** accounts are required to take the pipeline live on the cloud: **GitHub** (to run the daily cron job) and **Meta/Instagram** (to publish to your feed). Everything else (LLM, Flux images, Edge-TTS) runs with **zero login**.

### 5.1: How to Get a NEVER-EXPIRING Instagram Token (Workaround 6B)

Standard Meta user tokens expire every 60 days. Follow this exact workaround to generate a **System User Token** that **never expires**:

1. **Switch IG to Creator/Business (Free):** In the Instagram mobile app, go to *Settings and activity* $\rightarrow$ *Account type and tools* $\rightarrow$ *Switch to professional account*.
2. **Create a Free Meta Business App:**
   * Go to `https://developers.facebook.com/apps` and log in.
   * Click **Create App** $\rightarrow$ select **Other** $\rightarrow$ select **Business** $\rightarrow$ connect it to your Business Portfolio (Meta creates one automatically for free).
   * Inside the App Dashboard, click **Add Product** on **Instagram** (or **Instagram Graph API**).
3. **Bypass Facebook Page Linking (Optional Faster Path):**
   * Under **Instagram** $\rightarrow$ **API setup with Instagram login**, click **Add account** and log into your Instagram Creator account directly in the popup window.
   * Copy the **Instagram Account ID** (`IG_USER_ID`) displayed right next to your handle.
4. **Generate the Never-Expiring System User Token:**
   * Open `https://business.facebook.com/settings/system-users`.
   * Click **Add** $\rightarrow$ Name the user `AutoReelBot` and set Role to **Admin**.
   * Click **Assign Assets** $\rightarrow$ select your **App** and your **Instagram Account** and toggle **Manage account / Publish content**.
   * Click **Generate New Token** $\rightarrow$ select your App $\rightarrow$ set **Token Expiration** to **Never** $\rightarrow$ check `instagram_business_basic` and `instagram_business_content_publish` (or `instagram_basic` and `instagram_content_publish`).
   * Copy the token and save it as `IG_ACCESS_TOKEN`. Because it is a System User token with expiration set to **Never**, your workflow will run for years without re-authentication.

### 5.2: Optional Free Hugging Face Token (Workaround 4A)

If you set `USE_HF_ZEROGPU: "1"` to enable neural Image-to-Video motion via Hugging Face ZeroGPU:

1. Create a free account at `https://huggingface.co/join`.
2. Visit `https://huggingface.co/settings/tokens` $\rightarrow$ click **Create new token** $\rightarrow$ select **Read** $\rightarrow$ copy the `hf_...` token.
3. Add it as `HF_TOKEN` in your GitHub Repository Secrets.

### 5.3: Adding Secrets to GitHub Actions

1. Push this folder to a free GitHub repository (`https://github.com/new`).
2. In your GitHub repository, click **Settings** $\rightarrow$ **Secrets and variables** $\rightarrow$ **Actions** $\rightarrow$ **New repository secret**.
3. Add:
   * `IG_USER_ID`: Your 17-digit Instagram Account ID.
   * `IG_ACCESS_TOKEN`: Your Meta token from Step 5.1.
   * `HF_TOKEN`: *(Optional)* Your Hugging Face Read token from Step 5.2.
4. Go to the **Actions** tab in GitHub, select **Autonomous 90s AI Reel Workline**, and click **Run workflow** to trigger your first live cloud post immediately.

---

## 6. DETERMINISTIC TROUBLESHOOTING MATRIX

If any verification gate fails, match the error signature in the left column and execute the exact fix in the right column:

| Error Signature / Symptom | Root Cause | Exact Deterministic Fix |
| :--- | :--- | :--- |
| `json.decoder.JSONDecodeError` in `generate_storyboard` | Pollinations LLM returned conversational text around JSON | Built-in Workaround 1A/1B automatically strips outer text and cycles through `openai` $\rightarrow$ `mistral` $\rightarrow$ `llama`. Re-run once if all 3 endpoints had a transient network drop. |
| `HTTP Error 502` or `524` from `image.pollinations.ai` | Temporary overload on Flux endpoint | Built-in Workaround 2B automatically falls back from `model=flux` to `model=turbo` with a shifted seed. |
| `No such filter: 'subtitles'` in FFmpeg | Minimal FFmpeg binary compiled without `libass` | In `render_scene()`, replace `subtitles={rel_srt}:force_style=...` with `drawtext=text='90s AI Cinema':fontcolor=yellow:fontsize=42:x=(w-text_w)/2:y=h-250`. |
| `edge-tts: command not found` | Virtualenv binary path not resolved | Ensure `.venv/bin/pip install edge-tts` succeeded and run the script using `.venv/bin/python3 auto_reel.py`. |
| `Instagram container processing failed: ERROR` | Audio or video codec incompatibility | Verify `ffprobe final_reel.mp4` shows `h264` (`yuv420p`) and `aac` audio. Do not modify `-pix_fmt yuv420p` in `auto_reel.py`. |
| `OAuthException: Invalid OAuth access token` | Token expired or missing publish scope | Follow **Section 5.1 (Step 4)** to generate a **Never-Expiring System User Token** with `instagram_content_publish` enabled. |