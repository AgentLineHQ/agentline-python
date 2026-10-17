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
unless overridden at the agent level or per-call.

Returns account_id, default_voice_id (the stored preset name or UUID,
null when none is set) and resolved_voice_id (the voice UUID calls will
actually use).
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
their own voice_id configured), starting with their next call. The
previous value is not kept: read it with get_account_voice first if it
may be needed again.

Returns account_id, default_voice_id null, resolved_voice_id (the
system default) and a message.
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
  1. Per-call voice_id (make_outbound_call)
  2. Agent voice_id (update_agent)
  3. Account default (this tool)
  4. System default (Supportive Male)

Returns account_id, default_voice_id (as sent) and resolved_voice_id
(the UUID it resolves to). An unknown preset or malformed UUID returns
HTTP 400.
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

**voice_id:** `str` — Default voice for the account: a preset_name such as 'female-1' or a voice_id UUID, both listed by list_available_voices.
    
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

Returns {"voices": [...], "default_voice_id", "usage_hint"}: each voice
has preset_name (e.g. "female-1"), voice_id (UUID), name and description.
Pass either preset_name or voice_id as voice_id to create_agent,
update_agent, make_outbound_call or set_account_voice.
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

Adds an agent to the account with its own system prompt, voice and
greeting. Creating an agent is free; it cannot call until it has a
number, so call buy_phone_number next with the returned id as agent_id.

Returns the new agent, including its id (agt_...). A voice_id that is
not a preset from list_available_voices or a voice UUID is rejected, as
is a transfer_number that differs from owner_phone (HTTP 400).
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

**voice_id:** `typing.Optional[str]` — TTS voice preset name (e.g. 'female-1', 'male-1') or a voice UUID; defaults to system voice if not set
    
</dd>
</dl>

<dl>
<dd>

**transfer_number:** `typing.Optional[str]` — Number a live call is transferred to. Only the owner phone is allowed, so leave it out or send the same E.164 number as owner_phone; setting owner_phone fills it in.
    
</dd>
</dl>

<dl>
<dd>

**voicemail_message:** `typing.Optional[str]` — Message the AI agent leaves if the call goes to voicemail
    
</dd>
</dl>

<dl>
<dd>

**owner_phone:** `typing.Optional[str]` — Owner's phone number in E.164 format (e.g. '+12125551234'). Calls from this number enter task mode. This is also the only number a live call can be transferred to.
    
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

**agent_id:** `str` — Agent ID (agt_...) returned by create_agent or list_agents.
    
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

Permanently removes the agent with its calls and transcripts, messages,
conversations, contacts and webhook. Cannot be undone. Phone numbers
assigned to it are detached, not released: they stay active
on your account and can be reassigned to another agent.

Returns {"deleted": true, "agent_id": ...}.
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

**agent_id:** `str` — Agent ID (agt_...) returned by create_agent or list_agents.
    
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

Overwrites the fields you send; omitted fields keep their values and the
old values are not kept. Changes apply to the next inbound or outbound
call the agent handles; calls already in progress are unaffected.

Returns the full updated agent. Sending no fields, an unknown voice_id or
a transfer_number other than owner_phone returns HTTP 400.
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

**agent_id:** `str` — Agent ID (agt_...) returned by create_agent or list_agents.
    
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

**voice_id:** `typing.Optional[str]` — New TTS voice preset name or voice UUID
    
</dd>
</dl>

<dl>
<dd>

**transfer_number:** `typing.Optional[str]` — Number a live call is transferred to. Only the owner phone is allowed, so send the same E.164 number as owner_phone (current or in this request); setting owner_phone updates it automatically.
    
</dd>
</dl>

<dl>
<dd>

**voicemail_message:** `typing.Optional[str]` — Updated voicemail message
    
</dd>
</dl>

<dl>
<dd>

**owner_phone:** `typing.Optional[str]` — Updated owner phone in E.164. Also becomes the only live-call transfer destination.
    
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

Returns the current balance, currency, billing rates for calls,
phone numbers, and inbound SMS, plus what the balance can cover.
Use this to check affordability before paid telephony operations.
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

**period:** `typing.Optional[str]` — Which spending to total: 'current_month', 'last_month', 'all_time', or one calendar month as 'YYYY-MM' (e.g. '2026-09'). Unrecognized values fall back to the current month.
    
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

**agent_id:** `typing.Optional[str]` — Only calls handled by this agent (agt_... from list_agents). Omit for every agent on the account.
    
</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[str]` — Only calls in this exact status, e.g. 'completed' or 'failed'. Other statuses: 'initiated', 'in-progress', 'busy', 'no-answer', 'canceled'.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Page size: how many calls to return, newest first.
    
</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — How many calls to skip, to page past earlier results.
    
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

Dials a real person or business from the agent's number. The agent holds
the whole conversation on its own with its system prompt, voice and
greeting (or this call's overrides). The call reaches a third party and
is billed to the account at $0.10 per minute, first minute charged in
full, so confirm with the user first. Not idempotent: every successful
call dials again.

Prerequisites: an agent with an active number from buy_phone_number
(HTTP 400 otherwise), plus remaining subscription minutes or at least
$0.50 of wallet balance (HTTP 402 otherwise). Included minutes are used
first; only uncovered call time is charged to the wallet.

Returns right after dialing with the call id (call_...), agent_id,
from_number, to_number, direction, status and started_at; the call runs
on its own. Check get_call_details for progress and call
get_call_transcript once status is completed.
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

**voice_id:** `typing.Optional[str]` — Override the TTS voice for this call: preset name (e.g. 'female-1') or a voice UUID
    
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

**call_id:** `str` — Call ID (call_...) from make_outbound_call, list_calls or a call event.
    
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

A call.utterance or call.task.open event means a live caller is waiting.
Do the work, then push the facts; they reach the call immediately. The
hosted voice phrases them in its own words (it never reads your text
aloud) and keeps them for the rest of the call.

Body fields (send as arguments next to call_id):
  - context: the facts, e.g. "John emailed yesterday about an invoice."
    Aliases: summary, answer, response, reply, text, result, message.
  - disposition: partial (one real fact so far; spoken now, task stays
    open), progress (a note, not spoken, task stays open), done (default),
    failed or noop (settle the task; noop needs no context), or facts
    (call facts at any time without turn_id, e.g. a call-start briefing).
  - turn_id, push_token: as the parameters below.

Auth: pass the event's push_token as token. An AgentLine API key as
Authorization: Bearer also works; OAuth tokens do not.

Returns {"delivered": true, "status", "call_id", "turn_id"}; status
"duplicate" means an identical retry was already accepted. HTTP 409: the
turn is stale or cancelled, so do not reuse this context. HTTP 410: the
call ended; stop working on this request.
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

**call_id:** `str` — ID (call_...) of the live call, from the call.utterance or call.task.open event.
    
</dd>
</dl>

<dl>
<dd>

**request:** `typing.Dict[str, typing.Any]` 
    
</dd>
</dl>

<dl>
<dd>

**token:** `typing.Optional[str]` — The push_token from the call.utterance or call.task.open event. Authorizes this push for that call; same as the X-Push-Token header or a push_token body field.
    
</dd>
</dl>

<dl>
<dd>

**turn_id:** `typing.Optional[str]` — The exact turn_id from the event, identifying the question being answered. Can also be sent in the body. Required except for disposition=facts.
    
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

**call_id:** `str` — Call ID (call_...) from make_outbound_call, list_calls or a call event.
    
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

**call_id:** `str` — Call ID (call_...) from make_outbound_call, list_calls or a call event.
    
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
polled, they are automatically deleted from the mailbox, so process or
store them. Use peek_events to look without consuming.

Returns {"events": [...], "count"}: each event has event_id, agent_id,
event_type, payload and created_at, oldest first. An empty list means
nothing is pending. Agents with a webhook receive events there instead.
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

**agent_id:** `typing.Optional[str]` — Only events for this agent (agt_... from list_agents). Omit for every agent on the account.
    
</dd>
</dl>

<dl>
<dd>

**event_type:** `typing.Optional[str]` — Only events of this exact type, e.g. 'call.completed', 'call.failed', 'call.received' or 'sms.received'.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Most events to claim in this call, oldest first. Events past the limit stay queued for the next poll.
    
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

Returns {"pending_count", "events"}: pending_count counts every queued
event for the account (or agent_id); events lists event_id, agent_id,
event_type and created_at, without payloads. Call poll_events to get the
payloads.
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

**agent_id:** `typing.Optional[str]` — Only events for this agent (agt_... from list_agents). Omit for every agent on the account.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Most events to list, oldest first. Does not change pending_count.
    
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

**agent_id:** `typing.Optional[str]` — Only messages for this agent (agt_... from list_agents). Omit for every agent on the account.
    
</dd>
</dl>

<dl>
<dd>

**conversation_id:** `typing.Optional[str]` — Only messages in this thread; take conversation_id from an earlier list_messages result.
    
</dd>
</dl>

<dl>
<dd>

**limit:** `typing.Optional[int]` — Page size: how many messages to return, newest first.
    
</dd>
</dl>

<dl>
<dd>

**offset:** `typing.Optional[int]` — How many messages to skip, to page past earlier results.
    
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

Buy a US or Canadian phone number for your AI agent.

Buys a real +1 number from the carrier, attaches it to the agent and
uses an included subscription number, or charges $2.00 to the wallet. Once attached, the agent can make
outbound calls and answers inbound calls on this number. Existing numbers retain their carrier.
Each agent can have only one active number.

Prerequisites: an agent from create_agent with no active number (each
agent has at most one; a second purchase returns HTTP 409), plus a remaining
subscription number allowance or $2.00 in the wallet
(HTTP 402 otherwise; see get_account_balance).

Returns the number's id (num_..., used by release_phone_number and as
from_number_id), phone_number, country, number_type, status, cost,
balance_remaining and a private number card link (card_url,
card_image_url, card_url_expires_at). If the account has an owner email,
the card link is also emailed there.
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

**country:** `typing.Optional[str]` — Country code for the phone number ('US' or 'CA')
    
</dd>
</dl>

<dl>
<dd>

**number_type:** `typing.Optional[str]` — 'local' for a number in a geographic area code, or 'tollfree' for a toll-free 8xx number
    
</dd>
</dl>

<dl>
<dd>

**area_code:** `typing.Optional[str]` — For local numbers, the area code the number should be in, written as 3 digits (US e.g. '212' NYC, '415' SF; Canada e.g. '416' Toronto, '604' Vancouver, '514' Montreal); other values make the purchase fail. For tollfree, a prefix such as '800' or '888' narrows the search and other values are ignored. Omit to take any available number.
    
</dd>
</dl>

<dl>
<dd>

**pattern:** `typing.Optional[str]` — Legacy search: digits the local number must contain, e.g. '555'. Used only for local numbers when area_code is omitted; prefer area_code.
    
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

<details><summary><code>client.numbers.<a href="src/agentline_ai/numbers/client.py">attach</a>(...) -> typing.Any</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Manually attach a number that was bought outside this account.
Each agent can only have ONE active number.

Query params:
  - phone_number: E.164 format (e.g. "+12125551234")
  - agent_id: agent to attach to
  - country: "US" (default) or "CA" — both are +1, so say which
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

client.numbers.attach(
    phone_number="phone_number",
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

**phone_number:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**agent_id:** `str` 
    
</dd>
</dl>

<dl>
<dd>

**country:** `typing.Optional[str]` 
    
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

Returns the phone number, its assigned AI agent, country, and current status.
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
The full secret is only ever shown once, by set_webhook.

Returns {"webhooks": [...], "count"}: each has agent_id, url, masked
secret, signature_header, protocol, capabilities and created_at. An empty
list means no webhook is set, so events wait for poll_events. HTTP 404 if
agent_id is not an agent on this account.
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
webhook; setting it again replaces the URL. Omitted secret,
signature_header, protocol and capabilities keep their current values.

Returns agent_id, url, the full secret (shown only here; get_webhook
masks it), signature_header, protocol, capabilities and created_at.
Store the secret to verify the signature header on deliveries.
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

**agent_id:** `str` — ID (agt_...) of the agent whose events this webhook receives, from create_agent or list_agents. Each agent may have at most one webhook.
    
</dd>
</dl>

<dl>
<dd>

**secret:** `typing.Optional[str]` — Optional HMAC signing secret used to verify the signature header on delivered payloads. Omit to keep the current secret, or to auto-generate one for a new webhook.
    
</dd>
</dl>

<dl>
<dd>

**signature_header:** `typing.Optional[str]` — Header name for the HMAC-SHA256 signature of the raw body. Defaults to 'X-Webhook-Signature' (natively verified by Hermes, OpenClaw, and other agent platforms). Set to 'X-Hub-Signature-256' for GitHub-style verification, or any custom header name your platform expects. Omit to keep the existing value when updating.
    
</dd>
</dl>

<dl>
<dd>

**protocol:** `typing.Optional[WebhookConfigProtocol]` — Live relay protocol. 'agentline-relay/1' (default): one call.utterance POST per task, answer in the response body or via push. 'agentline-relay/2': typed POSTs (call.session.start, call.task.open, call.task.amend, call.task.cancel, call.session.end); answer only via POST /v1/calls/{call_id}/context and return 202 quickly. Omit to keep the existing value when updating.
    
</dd>
</dl>

<dl>
<dd>

**capabilities:** `typing.Optional[WebhookCapabilities]` — Relay v2 capabilities. Omit to keep the existing value when updating.
    
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

**agent_id:** `str` — Agent (agt_... from list_agents) whose configured webhook should receive the test event.
    
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

