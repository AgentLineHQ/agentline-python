# Reference
## Voice
<details><summary><code>client.voice.<a href="src/agentline_ai/voice/client.py">get</a>() -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the current account-level default voice for AI phone agents.

Returns which voice is used for all AI agents under this account
unless overridden at the agent level or per-call. Controls how
your AI agents sound during phone conversations.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.voice.get()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.voice.<a href="src/agentline_ai/voice/client.py">reset</a>() -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Reset account voice to the system default.

Removes the account-level voice override so all AI agents fall back
to the system default voice during phone calls (unless they have
their own voice_id configured).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.voice.reset()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.voice.<a href="src/agentline_ai/voice/client.py">set</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Set the account-level default voice for AI phone agents.

This becomes the default voice for ALL AI agents under this account,
controlling how they sound on phone calls. Individual agents or
specific calls can still override this setting.

Voice resolution priority:
  1. Per-call voice_id (POST /v1/calls)
  2. Agent voice_id (PATCH /v1/agents/{id})
  3. Account default (this endpoint)  ← you are here
  4. System default (Supportive Male)

Accepts:
  - A preset name: "female-1", "female-2", "female-3", "male-1", "male-2", "male-3"
  - A Cartesia voice UUID: "f786b574-daa5-4673-aa0c-cbe3e8534c02"
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.voice.set(
    voice_id="voice_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**voice_id:** `str` — TTS voice preset name (e.g. 'female-1', 'male-1') or Cartesia voice UUID
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.voice.<a href="src/agentline_ai/voice/client.py">list</a>() -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all available voice presets for AI phone agents.

Returns named TTS (text-to-speech) voice presets that can be used
when configuring AI agents or making phone calls. Each voice defines
how your AI agent sounds on the phone.

You can use a preset name (e.g. "female-1", "male-1") or pass any
valid Cartesia voice UUID directly as a voice_id.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.voice.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Agents
<details><summary><code>client.agents.<a href="src/agentline_ai/agents/client.py">list</a>() -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all AI voice agents configured on your account.

Returns every AI phone agent you've created, including their
system prompts, voice settings, and associated phone numbers.
Useful for checking which agents are ready to make or receive calls.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.agents.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.agents.<a href="src/agentline_ai/agents/client.py">create</a>(...) -> AgentOut</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new AI voice agent for telephony.

Sets up a new AI phone agent with a custom system prompt, voice,
and greeting. Once created, buy a phone number and attach it to
this agent so it can make and receive calls autonomously.

Fields:
  - name: Display name for the agent
  - system_prompt: Instructions that define the agent's personality and behavior on calls
  - initial_greeting: What the AI agent says when the call connects
  - voice_id: TTS voice preset (e.g. "female-1") or Cartesia UUID
  - transfer_number: Phone number to transfer calls to (e.g. a human operator)
  - voicemail_message: Message the agent leaves if the call goes to voicemail
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.agents.create(
    name="name",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` — Display name for the AI voice agent
    
</dd>
</dl>

<dl>
<dd>

**system_prompt:** `typing.Optional[str]` — Default instructions for the agent's personality and behavior on ALL calls (inbound and outbound). Can be overridden per-call via POST /v1/calls.
    
</dd>
</dl>

<dl>
<dd>

**initial_greeting:** `typing.Optional[str]` — Default opening line spoken on ALL calls (inbound and outbound), e.g. 'Hello, how can I help you today?'. Can be overridden per-call via POST /v1/calls.
    
</dd>
</dl>

<dl>
<dd>

**voice_id:** `typing.Optional[str]` — TTS voice preset name (e.g. 'female-1', 'male-1') or Cartesia voice UUID; defaults to system voice if not set
    
</dd>
</dl>

<dl>
<dd>

**transfer_number:** `typing.Optional[str]` — Phone number in E.164 format to transfer calls to (e.g. a human operator fallback)
    
</dd>
</dl>

<dl>
<dd>

**voicemail_message:** `typing.Optional[str]` — Message the AI agent leaves if the call goes to voicemail
    
</dd>
</dl>

<dl>
<dd>

**owner_phone:** `typing.Optional[str]` — Owner's phone number in E.164 format (e.g. '+12125551234'). Calls from this number enter task mode — the agent treats speech as executable instructions.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.agents.<a href="src/agentline_ai/agents/client.py">get</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of a specific AI voice agent.

Returns the agent's full configuration including system prompt,
voice settings, greeting, and transfer number.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.agents.get(
    agent_id="agent_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.agents.<a href="src/agentline_ai/agents/client.py">delete</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete an AI voice agent.

Permanently removes the agent and detaches any phone numbers
assigned to it. Detached numbers remain active on your account
and can be reassigned to another agent.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.agents.delete(
    agent_id="agent_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.agents.<a href="src/agentline_ai/agents/client.py">update</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an AI voice agent's configuration.

Modify any combination of the agent's settings: system prompt,
voice, greeting, transfer number, or voicemail message.
Changes take effect on the next call the agent handles.
Only include the fields you want to change — unset fields are preserved.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.agents.update(
    agent_id="agent_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — New display name for the AI voice agent
    
</dd>
</dl>

<dl>
<dd>

**system_prompt:** `typing.Optional[str]` — Updated default instructions for ALL future calls (does not affect calls already in progress)
    
</dd>
</dl>

<dl>
<dd>

**initial_greeting:** `typing.Optional[str]` — Updated default greeting for ALL future calls (inbound and outbound)
    
</dd>
</dl>

<dl>
<dd>

**voice_id:** `typing.Optional[str]` — New TTS voice preset name or Cartesia voice UUID
    
</dd>
</dl>

<dl>
<dd>

**transfer_number:** `typing.Optional[str]` — Updated transfer phone number in E.164 format
    
</dd>
</dl>

<dl>
<dd>

**voicemail_message:** `typing.Optional[str]` — Updated voicemail message
    
</dd>
</dl>

<dl>
<dd>

**owner_phone:** `typing.Optional[str]` — Updated owner phone number in E.164 format for task mode
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Billing
<details><summary><code>client.billing.<a href="src/agentline_ai/billing/client.py">get_balance</a>() -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get your AI telephony account balance and rate card.

Returns the current balance, currency, billing rates for calls
and phone numbers, and how many call minutes or phone numbers
the balance can cover. Use this to check affordability before
making calls or buying numbers for your AI agents.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.billing.get_balance()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.<a href="src/agentline_ai/billing/client.py">get_expenditure</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get a detailed expenditure breakdown for AI telephony usage.

Shows total spend split by category (voice calls, phone number
provisioning, top-ups, refunds) with counts and averages.
Useful for tracking how much your AI agents are spending on
phone calls and phone numbers.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.billing.get_expenditure()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**period:** `typing.Optional[str]` — Time period: 'current_month', 'last_month', 'all_time', or 'YYYY-MM'
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.<a href="src/agentline_ai/billing/client.py">list_call_charges</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List individual call charges from AI agent phone calls.

Each entry includes the voice call duration, cost, direction
(inbound/outbound), phone numbers involved, and timestamp.
Shows exactly how much each AI agent call cost.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.billing.list_call_charges()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Maximum number of call charges to return (1-200)
    
</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Number of records to skip for pagination
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.<a href="src/agentline_ai/billing/client.py">list_number_charges</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List phone number provisioning charges.

Shows the cost of each phone number bought for your AI agents,
including the number, country, and current status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.billing.list_number_charges()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Maximum number of number charges to return (1-200)
    
</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Number of records to skip for pagination
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.<a href="src/agentline_ai/billing/client.py">get_summary</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Month-over-month spending summary.

Returns total debits grouped by month for trend analysis.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.billing.get_summary()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**months:** `typing.Optional[int]` — Number of months to show
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Calls
<details><summary><code>client.calls.<a href="src/agentline_ai/calls/client.py">list</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List voice calls made by your AI agents.

Returns call history with optional filters by agent or status.
Each entry includes direction (inbound/outbound), duration,
phone numbers, and current status.

Filters:
  - agent_id: only calls for a specific AI agent
  - status: "initiated", "in-progress", "completed", or "failed"
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.calls.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `typing.Optional[str]` — Filter calls by AI agent ID
    
</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[str]` — Filter by call status: 'initiated', 'in-progress', 'completed', or 'failed'
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Maximum number of calls to return (1-200)
    
</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Number of calls to skip for pagination
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="src/agentline_ai/calls/client.py">create</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Make an outbound phone call from your AI agent.

Initiates a real phone call from the AI agent's phone number to the
specified destination. The agent uses its configured system prompt,
voice, and greeting to conduct the conversation autonomously.

The AI agent handles the entire call — speech-to-text, LLM reasoning,
and text-to-speech — in real time. The call transcript is saved
automatically and can be retrieved via GET /v1/calls/{call_id}/transcript.

Request body:
  - agent_id: the AI agent making the call
  - to_number: destination phone number in E.164 format (e.g. "+12125551234")
  - from_number_id: (optional) specific number to call from
  - system_prompt: (optional) override the agent's default prompt for this call
  - initial_greeting: (optional) override the agent's greeting for this call
  - voice_id: (optional) override the voice for this call
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.calls.create(
    agent_id="agent_id",
    to_number="to_number",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `str` — ID of the AI agent making the call (e.g. 'agt_abc123')
    
</dd>
</dl>

<dl>
<dd>

**to_number:** `str` — Destination phone number in E.164 format (e.g. '+12125551234')
    
</dd>
</dl>

<dl>
<dd>

**system_prompt:** `typing.Optional[str]` — Per-call system prompt override. Replaces the agent's default prompt for this call ONLY. If omitted, the agent's default system_prompt is used.
    
</dd>
</dl>

<dl>
<dd>

**initial_greeting:** `typing.Optional[str]` — Per-call greeting override. Replaces the agent's default greeting for this call ONLY. If omitted, the agent's default initial_greeting is used.
    
</dd>
</dl>

<dl>
<dd>

**voice_id:** `typing.Optional[str]` — Override the TTS voice for this call: preset name (e.g. 'female-1') or Cartesia UUID
    
</dd>
</dl>

<dl>
<dd>

**from_number_id:** `typing.Optional[str]` — Specific phone number ID to call from; defaults to the agent's assigned number
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="src/agentline_ai/calls/client.py">get</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get full details of a specific voice call.

Returns the call's metadata including direction, phone numbers,
status, duration, AI agent configuration used, and the full
conversation transcript between the AI agent and the caller.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.calls.get(
    call_id="call_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="src/agentline_ai/calls/client.py">push_context</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Push context into a LIVE relay-mode call (mid-call context injection).

This is the required way for backend agents (Hermes, OpenClaw, etc.) to
answer a live caller after a ``call.utterance`` event. Do your work, then
POST facts here — do NOT only send the answer to WhatsApp/SMS/chat.

AUTHENTICATION (one of):
  1. **Push token** (preferred — no API key): the ``push_token`` from the
     ``call.utterance`` payload, via ``X-Push-Token`` header, ``?token=``
     query param, or ``push_token`` body field.
  2. **Bearer API key**: ``Authorization: Bearer al_live_...`` for the
     account that owns the call.

Body — any of these keys works (``context`` is canonical):
    {"context": "the facts/answer the voice agent should speak"}

Other accepted keys: ``summary``, ``answer``, ``response``, ``message``,
``reply``, ``text``, ``result``.

Returns:
    delivered=true, status="live"     — voice agent will speak it now
    delivered=true, status="buffered" — caller moved on; held for their
      next question (late pushes are NOT rejected)
    HTTP 410                           — **call has ended.** STOP working
      on this request and abandon any in-flight lookup. No further context
      will be spoken.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.calls.push_context(
    call_id="call_id",
    request={
        "key": "value"
    },
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request:** `typing.Dict[str, typing.Any]` 
    
</dd>
</dl>

<dl>
<dd>

**token:** `typing.Optional[str]` — Push token (alt to X-Push-Token header / body).
    
</dd>
</dl>

<dl>
<dd>

**push_token:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="src/agentline_ai/calls/client.py">hangup</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Hang up an active phone call.

Programmatically terminates an in-progress voice call. Use this
when the AI agent needs to end the conversation, or to force-stop
a call that is no longer needed. The call's final transcript and
billing are processed automatically after hangup.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.calls.hangup(
    call_id="call_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.calls.<a href="src/agentline_ai/calls/client.py">get_transcript</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the full conversation transcript for a call.

Returns the complete speech-to-text transcript of the phone call,
with each turn labeled by role ("human" for the caller, "assistant"
for the AI agent). Useful for reviewing what was said on the call,
extracting information, or auditing AI agent behavior.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.calls.get_transcript(
    call_id="call_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Events
<details><summary><code>client.events.<a href="src/agentline_ai/events/client.py">poll</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Poll for telephony events from your AI agents.

Returns pending events such as call completions, transcripts, and
failures. Events are consumed on retrieval (one-time read) — once
polled, they are automatically deleted from the mailbox.

Your AI agent should call this endpoint periodically to receive
notifications about completed calls and their transcripts.

Filters:
  - agent_id: only events for a specific AI agent
  - event_type: e.g. "call.completed", "call.failed"
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.events.poll()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `typing.Optional[str]` — Filter events by AI agent ID
    
</dd>
</dl>

<dl>
<dd>

**event_type:** `typing.Optional[str]` — Filter by event type (e.g. 'call.completed', 'call.failed')
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Maximum number of events to return (1-200)
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.events.<a href="src/agentline_ai/events/client.py">peek</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Peek at pending telephony events without consuming them.

Returns a preview of queued events (call completions, transcripts)
without removing them from the mailbox. Useful for checking if
there are events to process before committing to retrieve them.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.events.peek()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `typing.Optional[str]` — Filter events by AI agent ID
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Maximum number of events to preview (1-200)
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Messages
<details><summary><code>client.messages.<a href="src/agentline_ai/messages/client.py">list</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List SMS messages sent and received by your AI agents.

Returns message history with optional filters by AI agent or
conversation. Each entry includes direction (inbound/outbound),
phone numbers, message body, and delivery status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.messages.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `typing.Optional[str]` — Filter messages by AI agent ID
    
</dd>
</dl>

<dl>
<dd>

**conversation_id:** `typing.Optional[str]` — Filter messages by conversation thread ID
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Maximum number of messages to return (1-200)
    
</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — Number of messages to skip for pagination
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.messages.<a href="src/agentline_ai/messages/client.py">send</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Send an outbound SMS message from an AI agent's phone number.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.messages.send(
    agent_id="agent_id",
    to_number="to_number",
    body="body",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `str` — ID of the AI agent sending the SMS (e.g. 'agt_abc123')
    
</dd>
</dl>

<dl>
<dd>

**to_number:** `str` — Destination phone number in E.164 format (e.g. '+12125551234')
    
</dd>
</dl>

<dl>
<dd>

**body:** `str` — SMS message text content
    
</dd>
</dl>

<dl>
<dd>

**media_url:** `typing.Optional[str]` — URL of media to attach (MMS)
    
</dd>
</dl>

<dl>
<dd>

**from_number_id:** `typing.Optional[str]` — Specific phone number ID to send from; defaults to the agent's assigned number
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.messages.<a href="src/agentline_ai/messages/client.py">list_conversations</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all SMS conversations for your AI agents.

Returns conversation threads, optionally filtered by AI agent.
Each conversation represents an ongoing SMS exchange between
an AI agent's phone number and an external contact.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.messages.list_conversations()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Numbers
<details><summary><code>client.numbers.<a href="src/agentline_ai/numbers/client.py">list</a>() -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List all phone numbers provisioned on your account.

Returns every phone number you've bought for your AI agents,
including which agent each number is assigned to, the number's
status (active/released), and country.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.numbers.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="src/agentline_ai/numbers/client.py">buy</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Buy a US phone number for your AI agent.

Searches for and purchases a real US phone number from the telephony
provider, then attaches it to the specified AI agent. Once attached,
the agent can make outbound calls and receive inbound calls on this number.

Each AI agent can only have ONE active phone number. Costs $2.00 per number.

Request body:
  - agent_id: str (required) — the AI agent to assign this number to
  - country: str (must be "US")
  - number_type: "local" | "tollfree"
  - area_code: preferred 3-digit US area code (e.g. "212" for NYC, "415" for SF)
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.numbers.buy(
    agent_id="agent_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `str` — ID of the AI agent to assign this phone number to (e.g. 'agt_abc123')
    
</dd>
</dl>

<dl>
<dd>

**country:** `typing.Optional[str]` — Country code for the phone number (currently only 'US' is supported)
    
</dd>
</dl>

<dl>
<dd>

**number_type:** `typing.Optional[str]` — Type of phone number: 'local' or 'tollfree'
    
</dd>
</dl>

<dl>
<dd>

**area_code:** `typing.Optional[str]` — Preferred 3-digit US area code (e.g. '212' for NYC, '415' for SF, '310' for LA)
    
</dd>
</dl>

<dl>
<dd>

**pattern:** `typing.Optional[str]` — Legacy digit pattern match (prefer area_code instead)
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="src/agentline_ai/numbers/client.py">get</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get details of a specific phone number.

Returns the phone number, its assigned AI agent, provider ID,
country, and current status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.numbers.get(
    number_id="number_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**number_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="src/agentline_ai/numbers/client.py">reassign</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Reassign a phone number to a different AI agent.

Moves an existing phone number from one AI agent to another.
The target agent must not already have an active number assigned.
The phone number remains active — only the agent ownership changes.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.numbers.reassign(
    number_id="number_id",
    agent_id="agent_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**number_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**agent_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks
<details><summary><code>client.webhooks.<a href="src/agentline_ai/webhooks/client.py">list</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the account's per-agent webhook configuration(s).

Secrets are **masked**. Pass `agent_id` to inspect a single agent's webhook.
The full secret is only ever shown once, on the POST that creates/replaces it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.webhooks.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `typing.Optional[str]` — Inspect one agent's webhook (omit to list all)
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="src/agentline_ai/webhooks/client.py">set</a>(...) -> WebhookCreated</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create or replace an agent's webhook.

The configured URL receives ALL of that agent's event types — call lifecycle
(`call.received`, `call.completed`, `call.failed`), SMS (`sms.received`),
and future events — as signed JSON POSTs. Each agent may have at most one
webhook; POSTing again replaces it.

- `agent_id`: the agent whose events this webhook receives (required).
- `secret`:   HMAC signing secret. Omit to auto-generate.

The response returns the full `secret` **once** — store it to verify the
signature header on deliveries.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.webhooks.set(
    url="url",
    agent_id="agent_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**url:** `str` — HTTPS URL that will receive this agent's events as signed JSON POSTs. Setting this replaces any existing webhook for the agent.
    
</dd>
</dl>

<dl>
<dd>

**agent_id:** `str` — ID of the agent whose events this webhook receives. Each agent may have at most one webhook.
    
</dd>
</dl>

<dl>
<dd>

**secret:** `typing.Optional[str]` — Optional HMAC signing secret. Auto-generated if omitted. Used to verify the signature header on delivered payloads.
    
</dd>
</dl>

<dl>
<dd>

**signature_header:** `typing.Optional[str]` — Header name for the HMAC-SHA256 signature of the raw body. Defaults to 'X-Webhook-Signature' (natively verified by Hermes, OpenClaw, and other agent platforms). Set to 'X-Hub-Signature-256' for GitHub-style verification, or any custom header name your platform expects. Omit to keep the existing value when updating.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="src/agentline_ai/webhooks/client.py">delete</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Remove an agent's webhook. No events for that agent will be delivered via
HTTP afterwards; they remain available via GET /v1/events (the mailbox).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.webhooks.delete(
    agent_id="agent_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `str` — Agent whose webhook to delete
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webhooks.<a href="src/agentline_ai/webhooks/client.py">test</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fire a signed `webhook.test` event to the agent's webhook.

Uses the exact same event bus (publish_event) that real telephony events use,
so a successful delivery confirms the entire pipeline is wired correctly.
Returns 404 if no webhook is configured for the agent.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from agentline_ai import AgentLine
from agentline_ai.environment import AgentLineEnvironment

client = AgentLine(
    api_key="<token>",
    environment=AgentLineEnvironment.PRODUCTION,
)

client.webhooks.test(
    agent_id="agent_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**agent_id:** `str` — Agent whose webhook to test
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

