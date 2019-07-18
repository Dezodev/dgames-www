<template lang="html">
	<div class="">
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequuntur, libero, labore. Dolore suscipit iure veniam. Esse quod sapiente dolorem sequi rerum delectus eius obcaecati quam, itaque atque quidem fugit rem.</p>
		<p>Consectetur architecto, delectus non voluptas quae rem voluptatem distinctio quas voluptate ad excepturi ea doloremque qui minima quo, numquam assumenda iusto fugit ipsum sed dolorum eveniet. Asperiores optio ea quisquam?</p>

		<h2 id="buttons">Boutons</h2>

		<div>
			<a-button type="primary">Primary</a-button>
			<a-button>Default</a-button>
			<a-button type="dashed">Dashed</a-button>
			<a-button type="danger">Danger</a-button>
		</div>
		<div :style="{ marginTop: '20px' }">
			<a-button type="primary" ghost>Primary</a-button>
			<a-button ghost>Default</a-button>
			<a-button type="dashed" ghost>Dashed</a-button>
			<a-button type="danger" ghost>danger</a-button>
		</div>

		<h2>Breadcrumb</h2>

		<div class="mt-2">
			<a-breadcrumb>
				<a-breadcrumb-item>Home</a-breadcrumb-item>
				<a-breadcrumb-item><a href="">Application Center</a></a-breadcrumb-item>
				<a-breadcrumb-item><a href="">Application List</a></a-breadcrumb-item>
				<a-breadcrumb-item>An Application</a-breadcrumb-item>
			</a-breadcrumb>
		</div>

		<h2>Dropdown</h2>

		<div class="">
			<a-dropdown :trigger="['click']">
				<a class="ant-dropdown-link" href="#">
					Click me <a-icon type="down" />
				</a>
				<a-menu slot="overlay">
					<a-menu-item key="0">
						<a href="http://www.alipay.com/">1st menu item</a>
					</a-menu-item>
					<a-menu-item key="1">
						<a href="http://www.taobao.com/">2nd menu item</a>
					</a-menu-item>
					<a-menu-divider />
					<a-menu-item key="3">3rd menu item</a-menu-item>
				</a-menu>
			</a-dropdown>
		</div>

		<h2>Pagination</h2>

		<div class="">
			<a-pagination :value="3" :total="50" />
		</div>

		<h2>Steps</h2>
		<div>
			<a-steps :current="1">
				<a-step>
					<template slot="title">Finished</template>
					<span slot="description">This is a description.</span>
				</a-step>
				<a-step title="In Progress" description="This is a description." />
				<a-step title="Waiting" description="This is a description." />
			</a-steps>
		</div>

		<h2>Forms</h2>
		<div>
			<a-form
				id="components-form-demo-validate-other"
				:form="form"
				@submit="handleSubmit"
				>

				<h3>General</h3>
				<a-form-item
					v-bind="formItemLayout"
					label="E-mail"
					>
					<a-input
						v-decorator="[
						'email',
						{
							rules: [{
							type: 'email', message: 'The input is not valid E-mail!',
						}, {
							required: true, message: 'Please input your E-mail!',
						}]
						}
						]"
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Password"
					>
					<a-input
						v-decorator="[
						'password',
						{
						rules: [{
						required: true, message: 'Please input your password!',
						}, {
						validator: validateToNextPassword,
						}],
						}
						]"
						type="password"
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Confirm Password"
					>
					<a-input
						v-decorator="[
						'confirm',
						{
						rules: [{
						required: true, message: 'Please confirm your password!',
						}, {
						validator: compareToFirstPassword,
						}],
						}
						]"
						type="password"
						@blur="handleConfirmBlur"
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					>
					<span slot="label">
						Nickname&nbsp;
						<a-tooltip title="What do you want others to call you?">
							<a-icon type="question-circle-o" />
						</a-tooltip>
					</span>
					<a-input
						v-decorator="[
						'nickname',
						{
						rules: [{ required: true, message: 'Please input your nickname!', whitespace: true }]
						}
						]"
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Habitual Residence"
					>
					<a-cascader
						v-decorator="[
						'residence',
						{
						initialValue: ['zhejiang', 'hangzhou', 'xihu'],
						rules: [{ type: 'array', required: true, message: 'Please select your habitual residence!' }],
						}
						]"
						:options="residences"
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Phone Number"
					>
					<a-input
						v-decorator="[
						'phone',
						{
						rules: [{ required: true, message: 'Please input your phone number!' }],
						}
						]"
						style="width: 100%"
						>
						<a-select
							slot="addonBefore"
							v-decorator="[
							'prefix',
							{ initialValue: '86' }
							]"
							style="width: 70px"
							>
							<a-select-option value="86">
								+86
							</a-select-option>
							<a-select-option value="87">
								+87
							</a-select-option>
						</a-select>
					</a-input>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Website"
					>
					<a-auto-complete
						v-decorator="[
						'website',
						{rules: [{ required: true, message: 'Please input website!' }]}
						]"
						placeholder="website"
						>
						<template slot="dataSource">
							<a-select-option
								v-for="website in autoCompleteResult"
								:key="website"
								>
								{{ website }}
							</a-select-option>
						</template>
						<a-input />
					</a-auto-complete>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Captcha"
					extra="We must make sure that your are a human."
					>
					<a-row :gutter="8">
						<a-col :span="12">
							<a-input
								v-decorator="[
								'captcha',
								{rules: [{ required: true, message: 'Please input the captcha you got!' }]}
								]"
								/>
						</a-col>
						<a-col :span="12">
							<a-button>Get captcha</a-button>
						</a-col>
					</a-row>
				</a-form-item>
				<a-form-item v-bind="tailFormItemLayout">
					<a-checkbox
						v-decorator="['agreement', {valuePropName: 'checked'}]"
						>
						I have read the <a href="">
						agreement
						</a>
					</a-checkbox>
				</a-form-item>

				<h3>Datepicker</h3>
				<a-form-item
					v-bind="formItemLayout"
					label="DatePicker"
					>
					<a-date-picker v-decorator="['date-picker', config]" />
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="DatePicker[showTime]"
					>
					<a-date-picker
						v-decorator="['date-time-picker', config]"
						show-time
						format="YYYY-MM-DD HH:mm:ss"
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="MonthPicker"
					>
					<a-monthPicker v-decorator="['month-picker', config]" />
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="RangePicker"
					>
					<a-range-picker v-decorator="['range-picker', rangeConfig]" />
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="RangePicker[showTime]"
					>
					<a-range-picker
						v-decorator="['range-time-picker', rangeConfig]"
						show-time
						format="YYYY-MM-DD HH:mm:ss"
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="TimePicker"
					>
					<a-time-picker v-decorator="['time-picker', config]" />
				</a-form-item>

				<h3>Other Form Controls</h3>
				<a-form-item
					v-bind="formItemLayout"
					label="Plain Text"
					>
					<span class="ant-form-text">
					China
					</span>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Select"
					has-feedback
					>
					<a-select
						v-decorator="[
						'select',
						{rules: [{ required: true, message: 'Please select your country!' }]}
						]"
						placeholder="Please select a country"
						>
						<a-select-option value="china">
							China
						</a-select-option>
						<a-select-option value="usa">
							U.S.A
						</a-select-option>
					</a-select>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Select[multiple]"
					>
					<a-select
						v-decorator="[
						'select-multiple', {
						rules: [{ required: true, message: 'Please select your favourite colors!', type: 'array' }],
						}
						]"
						mode="multiple"
						placeholder="Please select favourite colors"
						>
						<a-select-option value="red">
							Red
						</a-select-option>
						<a-select-option value="green">
							Green
						</a-select-option>
						<a-select-option value="blue">
							Blue
						</a-select-option>
					</a-select>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="InputNumber"
					>
					<a-input-number
						v-decorator="['input-number', { initialValue: 3 }]"
						:min="1"
						:max="10"
						/>
					<span class="ant-form-text">
					machines
					</span>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Switch"
					>
					<a-switch v-decorator="['switch', { valuePropName: 'checked' }]" />
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Slider"
					>
					<a-slider
						v-decorator="['slider']"
						:marks="{ 0: 'A', 20: 'B', 40: 'C', 60: 'D', 80: 'E', 100: 'F' }"
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Radio.Group"
					>
					<a-radio-group v-decorator="['radio-group']">
						<a-radio value="a">
							item 1
						</a-radio>
						<a-radio value="b">
							item 2
						</a-radio>
						<a-radio value="c">
							item 3
						</a-radio>
					</a-radio-group>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Radio.Button"
					>
					<a-radio-group v-decorator="['radio-button']">
						<a-radio-button value="a">
							item 1
						</a-radio-button>
						<a-radio-button value="b">
							item 2
						</a-radio-button>
						<a-radio-button value="c">
							item 3
						</a-radio-button>
					</a-radio-group>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Checkbox.Group"
					>
					<a-checkbox-group
						v-decorator="['checkbox-group', {initialValue: ['A', 'B']}]"
						style="width: 100%;"
						>
						<a-row>
							<a-col :span="8">
								<a-checkbox value="A">
									A
								</a-checkbox>
							</a-col>
							<a-col :span="8">
								<a-checkbox
									disabled
									value="B"
									>
									B
								</a-checkbox>
							</a-col>
							<a-col :span="8">
								<a-checkbox value="C">
									C
								</a-checkbox>
							</a-col>
							<a-col :span="8">
								<a-checkbox value="D">
									D
								</a-checkbox>
							</a-col>
							<a-col :span="8">
								<a-checkbox value="E">
									E
								</a-checkbox>
							</a-col>
						</a-row>
					</a-checkbox-group>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Rate"
					>
					<a-rate
						v-decorator="['rate', {initialValue: 3.5}]"
						allow-half
						/>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Upload"
					extra="longgggggggggggggggggggggggggggggggggg"
					>
					<a-upload
						v-decorator="['upload', {
						valuePropName: 'fileList',
						getValueFromEvent: normFile,
						}]"
						name="logo"
						action="/upload.do"
						list-type="picture"
						>
						<a-button>
							<a-icon type="upload" />
							Click to upload
						</a-button>
					</a-upload>
				</a-form-item>
				<a-form-item
					v-bind="formItemLayout"
					label="Dragger"
					>
					<div class="dropbox">
						<a-upload-dragger
							v-decorator="['dragger', {
							valuePropName: 'fileList',
							getValueFromEvent: normFile,
							}]"
							name="files"
							action="/upload.do"
							>
							<p class="ant-upload-drag-icon">
								<a-icon type="inbox" />
							</p>
							<p class="ant-upload-text">
								Click or drag file to this area to upload
							</p>
							<p class="ant-upload-hint">
								Support for a single or bulk upload.
							</p>
						</a-upload-dragger>
					</div>
				</a-form-item>
				<a-form-item
					:wrapper-col="{ span: 12, offset: 6 }"
					>
					<a-button
						type="primary"
						html-type="submit"
						>
						Submit
					</a-button>
				</a-form-item>
			</a-form>
		</div>

		<h2>Select</h2>
		<div>
			<a-select defaultValue="lucy" style="width: 120px" @change="handleChange">
				<a-select-option value="jack">Jack</a-select-option>
				<a-select-option value="lucy">Lucy</a-select-option>
				<a-select-option value="disabled" disabled>Disabled</a-select-option>
				<a-select-option value="Yiminghe">yiminghe</a-select-option>
			</a-select>
		</div>
	</div>
</template>

<script>
export default {
	data () {
		return {
			formItemLayout: {
				labelCol: { span: 6 },
				wrapperCol: { span: 14 },
			},
		}
	},
	methods: {
		onChange () {

		}
	}
}
</script>
